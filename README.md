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

Przeliczenie Farenhaity na Felciusze z wyborem
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
