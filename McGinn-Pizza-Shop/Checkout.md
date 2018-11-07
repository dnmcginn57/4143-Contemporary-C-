```csharp
//David McGinn
//11-7-18
//CMPS4143
//This form accepts the pizza array list
//  and total, and displays the recipt accordingly

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
    public partial class Checkout : Form
    {
        private string _orderReciept;
        private double _total;
        public bool _doClear = false;

        public Checkout(ArrayList pizza, double tot)
        {
            InitializeComponent();
            _orderReciept = "";
            _total = tot;

            foreach(Pizza p in pizza)
            {
                _orderReciept += p;
                _orderReciept += Environment.NewLine;
            }

            _orderReciept += Environment.NewLine;
            _orderReciept += Environment.NewLine;
            _orderReciept += "____________________________";
            _orderReciept += Environment.NewLine;
            _orderReciept += "Total:           $" + _total;
            ReciptText.Text = _orderReciept;
        }

        private void FinishOrder_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Your order is on the way");
            Application.Exit();
        }

        private void AddToOrder_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void ClearOrder_Click(object sender, EventArgs e)
        {
            _doClear = true;
            this.Close();
        }
    }
}

```
