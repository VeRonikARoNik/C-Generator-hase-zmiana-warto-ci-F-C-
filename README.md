# Generator Haseł
<img width="824" height="332" alt="image" src="https://github.com/user-attachments/assets/3fef1617-b264-475a-b626-ea6be09af4fd" />

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using static System.Windows.Forms.VisualStyles.VisualStyleElement.Rebar;

namespace GeneratorHasel
{
    public partial class Form1 : Form
    {
        Random rand = new Random();
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            int length = (int)numericUpDown1.Value;

            string letters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
            string digits = "0123456789";
            string specials = "!@#$%^&*()_+=-<>?/";

            string allowed = letters;

            if (checkBox1.Checked)
                allowed += digits;

            if (checkBox2.Checked)
                allowed += specials;

            if (string.IsNullOrEmpty(allowed))
            {
                MessageBox.Show("Wybierz przynajmniej jeden typ znaków!");
                return;
            }

            StringBuilder password = new StringBuilder();

            for (int i = 0; i < length; i++)
            {
                int index = rand.Next(allowed.Length);
                password.Append(allowed[index]);
            }

            textBox1.Text = password.ToString();
        }
    }
    }


```

# Przeliczenie Farenhaity na Felciusze z wyborem

<img width="546" height="278" alt="image" src="https://github.com/user-attachments/assets/9a53c280-cd31-4cb2-b027-083297a35c78" />

```
 using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace przeliczenie
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            if (!double.TryParse(textBox1.Text, out double input))
            {
                MessageBox.Show("Wpisz poprawną liczbę!");
                return;
            }

            double result;

            if (comboBox1.SelectedItem.ToString() == "C → F")
            {
                result = input * 1.8 + 32;
                label1.Text = $"Wynik: {result:F2} °F";
            }
            else
            {
                result = (input - 32) / 1.8;
                label1.Text = $"Wynik: {result:F2} °C";
            }
        }

        private void comboBox1_SelectedIndexChanged(object sender, EventArgs e)
        {

        }
    }
}

```


# Aplikacja szybka reakcja

<img width="699" height="513" alt="image" src="https://github.com/user-attachments/assets/b0e80ec7-ea0e-49c3-884b-1b4c87c55933" />


```
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Drawing;
using System.Windows.Forms;

namespace Rection_test
{
    public partial class Form1 : Form
    {
        Random rand = new Random();
        Stopwatch stopwatch = new Stopwatch();
        Timer timer = new Timer();

        List<int> scores = new List<int>();
        int bestScore = int.MaxValue;

        public Form1()
        {
            InitializeComponent();

            lblInfo.Text = "Kliknij START, aby rozpocząć test.";
            lblInfo.TextAlign = ContentAlignment.MiddleCenter;
            lblInfo.Font = new Font("Segoe UI", 14, FontStyle.Bold);

            lblBest.Text = "Najlepszy wynik: ---";

            listBox1.BackColor = Color.White;
            listBox1.ForeColor = Color.Black;
            listBox1.Font = new Font("Segoe UI", 12);

            timer.Tick += Timer_Tick;

            foreach (Control c in this.Controls)
            {
                c.MouseDown += ReactionClick;
            }
        }

        private void btnStart_Click(object sender, EventArgs e)
        {
            lblInfo.Text = "Czekaj...";
            this.BackColor = Color.Red;

            timer.Interval = rand.Next(1000, 3000);
            timer.Start();
        }

        private void Timer_Tick(object sender, EventArgs e)
        {
            timer.Stop();
            this.BackColor = Color.Lime;
            lblInfo.Text = "Kliknij teraz!";

            stopwatch.Reset();
            stopwatch.Start();

            this.MouseDown += ReactionClick;
        }

        private void ReactionClick(object sender, MouseEventArgs e)
        {
            stopwatch.Stop();
            this.MouseDown -= ReactionClick;

            int time = (int)stopwatch.ElapsedMilliseconds;

            lblInfo.Text = $"Twój czas reakcji: {time} ms";
            this.BackColor = Color.White;

            scores.Add(time);
            listBox1.Items.Add($"{time} ms");

            if (time < bestScore)
            {
                bestScore = time;
                lblBest.Text = $"Najlepszy wynik: {bestScore} ms";
            }
        }
    }
}


```

