```csharp
//David McGinn
//11-7-18
//CMPS4143
//The main form, which is always running, keeps track of the
//entire order. the running total.
//if the main form is closed the program terminates

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
    public partial class WelcomePage : Form
    {

        public ArrayList allPizza;
        private double _total = 0.0;
        private Specialties spec;
        private Custom cust;
        private Checkout chk;


        public WelcomePage()
        {
            InitializeComponent();
            allPizza = new ArrayList();
            spec = new Specialties();
            cust = new Custom();
        }

        private void ToSpecialties_Click(object sender, EventArgs e)
        {

            spec.ShowDialog();
            allPizza.Add(this.spec.curPizza);
            _total += spec.curPizza.Price;
            chk = new Checkout(allPizza, _total);
            chk.ShowDialog();
            if(chk._doClear == true)
            {
                allPizza.Clear();
            }

        }

        private void ToPizzaCreator_Click(object sender, EventArgs e)
        {

            cust.ShowDialog();
            allPizza.Add(this.cust.curPizza);
            _total += cust.curPizza.Price;
            chk = new Checkout(allPizza, _total);
            chk.ShowDialog();
            if (chk._doClear == true)
            {
                allPizza.Clear();
            }


        }

        public void AddPizza(Pizza p)
        {
            allPizza.Add(p);
        }
    }
}

```
