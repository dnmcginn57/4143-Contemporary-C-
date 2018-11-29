```csharp
//David McGinn
//11-30-18
//CMPS-4143
//This is a multi document interface that manages supplies
//  for multiple workshops at a science convention
//  Users may enter names of custom workshops
//      and manage individual supply lists for each workshop

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace McGinn_Program8_MDI
{
    public partial class ItemInformation : Form
    {
        public Record record;
        public ItemInformation()
        {
            InitializeComponent();
        }

        private void CancelItemButton_Click(object sender, EventArgs e)
        {
            this.Hide();
        }

        private void AddItemButton_Click(object sender, EventArgs e)
        {
            bool p;
            int quantity;
            double price;
            string name;

            //check validity of quantity input
            p = int.TryParse(QuantityBox.Text, out quantity);
            if (p)
            {
                p = double.TryParse(PriceBox.Text, out price);
                if (p)
                {
                    name = NameBox.Text;
                    if (name != null && name != "")
                    {
                        record = new Record(quantity, price, name);
                        this.Hide();
                    }
                    else
                        MessageBox.Show("Invalid Name",
                            "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
                else
                    MessageBox.Show("Invalid Price",
                        "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
            else
                MessageBox.Show("Invalid Quantity",
                    "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
        }
    }
}

```
