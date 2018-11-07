```csharp
//David McGinn
//11-7-18
//CMPS4143
//Similarly to the Specialties form; this form
//  is responsible for creating a pizza object for the
//  main form to store in it's arraylist
//  however in this from there are many custom
//  options for topping, crust type etc..

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Collections;

namespace McGinn_Pizza_Shop
{
    public partial class Custom : Form
    {
        private ArrayList _toppings;
        public Pizza curPizza;
        public Custom()
        {
            InitializeComponent();
        }

        private void CustConfirm_Click(object sender, EventArgs e)
        {
            string size = "";
            string crust = "";
            _toppings = new ArrayList();

            //add all types of sauces selected
            foreach (Control c in SauceMainPanel.Controls)
            {
                if((c is CheckBox) && ((CheckBox) c).Checked)
                {
                    _toppings.Add(c.Text);
                }
            }

            //add all types of cheese selected
            foreach (Control c in CheeseMainPanel.Controls)
            {
                if ((c is CheckBox) && ((CheckBox)c).Checked)
                {
                    _toppings.Add(c.Text);
                }
            }

            //add all veggies selected
            foreach (Control c in VegiMainPanel.Controls)
            {
                if ((c is CheckBox) && ((CheckBox)c).Checked)
                {
                    _toppings.Add(c.Text);
                }
            }

            //add all meats selected
            foreach (Control c in MeatMainPanel.Controls)
            {
                if ((c is CheckBox) && ((CheckBox)c).Checked)
                {
                    _toppings.Add(c.Text);
                }
            }


            //add all misc selected
            foreach (Control c in MiscMainPanel.Controls)
            {
                if ((c is CheckBox) && ((CheckBox)c).Checked)
                {
                    _toppings.Add(c.Text);
                }
            }

            //get the size
            RadioButton s = SizeBox.Controls.OfType<RadioButton>()
                .Where(x => x.Checked).FirstOrDefault();

            //get the crust
            RadioButton cr = CrustBox.Controls.OfType<RadioButton>()
                .Where(x => x.Checked).FirstOrDefault();

            size = s.Text;
            crust = cr.Text;

            curPizza = new Pizza("Custom", size, crust);
            curPizza.AddToppings(_toppings);

            this.Close();



        }
    }
}

```
