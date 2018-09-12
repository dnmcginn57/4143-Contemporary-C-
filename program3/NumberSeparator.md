```csharp
//David McGinn
//9-12-18
//cmps-4143
//This program is an app that allows the user to input
//  a 5 diget number.  the program then separates each character
//  by a space.


using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Program_3
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void GoButton_Click(object sender, EventArgs e)
        {
            string number = InputText.Text;
            string number2 = "";
            
            for (int i = 0; i < number.Length; i++)
            {
                number2 += number[i];
                number2 += " ";
            }

            OutBox.Text = number2;
        }
    }
}

```
