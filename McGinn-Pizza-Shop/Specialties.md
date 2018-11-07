```csharp
//David McGinn
//11-7-18
//CMPS4143
//The user may select from a list of
//  specialties and then select a size
//  this form generates a pizza object
//  which is read into the main form's
//  arraylist of pizzas

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
    public partial class Specialties : Form
    {
        public Pizza curPizza;

        public Specialties()
        {
            InitializeComponent();
        }

        private void SpecialtiesConfirm_Click(object sender, EventArgs e)
        {
            //type of pizza selected
            RadioButton n = MenuPanel.Controls.OfType<RadioButton>()
                .Where(x => x.Checked).FirstOrDefault();
            //name of selected pizzas
            RadioButton s = SizeBox.Controls.OfType<RadioButton>()
                .Where(x => x.Checked).FirstOrDefault();

            if(n == null || s == null)
            {
                MessageBox.Show("Please select both a size" +
                    " and a type of pizza");
                return;
            }

            //get a name and size for the Pizza
            string name, size;
            name = n.Text;
            size = s.Text;

            curPizza = new Pizza(name, size);

            this.Close();

        }
    }
}

```
