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
    public partial class WorkshopNameForm : Form
    {

        public string Workshopname;
        public WorkshopNameForm()
        {
            InitializeComponent();
        }

        private void NewFileCancelButton_Click(object sender, EventArgs e)
        {
            this.Close();
        }

        private void NameOK_Click(object sender, EventArgs e)
        {
            string newname = NewNameBox.Text;
            if (newname == "" || newname == null)
                MessageBox.Show("Invalid File Name", "Error",
                    MessageBoxButtons.OK, MessageBoxIcon.Error);
            else
            {
                Workshopname = newname;
                this.Hide();
            }
        }
    }
}

```
