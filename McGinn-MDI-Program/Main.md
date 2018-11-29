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
using System.IO;
using System.Runtime.Serialization;
using System.Runtime.Serialization.Formatters.Binary;

namespace McGinn_Program8_MDI
{
    public partial class WorkshopSupply : Form
    {

        private BinaryFormatter formatter = new BinaryFormatter();
        
        
        public WorkshopSupply()
        {
            InitializeComponent();
        }

        //Creates or opens a workshop
        private void newToolStripMenuItem_Click(object sender, EventArgs e)
        {
            FileStream output;
            string filename;
            WorkshopNameForm nameprompt = new WorkshopNameForm();

            nameprompt.ShowDialog();
            filename = nameprompt.Workshopname;
            nameprompt.Close();
            //check to make sure nameprompt exited with a valid name
            if (filename != null)
            {
                filename += ".sup";

                try
                {
                    output = new FileStream(filename,
                        FileMode.OpenOrCreate, FileAccess.Write);

                    output.Close();

                    WorkshopForm workshop = new WorkshopForm(filename);
                    workshop.MdiParent = this;
                    workshop.Show();
                }
                catch (System.NotSupportedException)
                {
                    MessageBox.Show("File name cann" +
                        "ot contain \\ / : * ? \" < > or | ",
                        "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }

        //closes the program
        private void exitToolStripMenuItem_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

        //Exclusively opens a workshop file through an open file dialog
        private void openToolStripMenuItem_Click(object sender, EventArgs e)
        {
            OpenFileDialog filechooser = new OpenFileDialog();
            DialogResult result = filechooser.ShowDialog();
            string filename;

            if(result != DialogResult.Cancel)
            {
                filename = filechooser.FileName;
                if(!filename.Contains(".sup"))
                {
                    MessageBox.Show("This is not a .sup file");
                }
                else
                {
                    WorkshopForm workshop = new WorkshopForm(filename);
                    workshop.MdiParent = this;
                    workshop.Show();
                }
            }
        }

        //Insert an item into the active child dialog
        private void insertToolStripMenuItem_Click(object sender, EventArgs e)
        {
            ItemInformation info = new ItemInformation();
            info.ShowDialog();
            info.Close();
            Record r = info.record;
            WorkshopForm active = ActiveMdiChild as WorkshopForm;
            if (r != null)
            {
                active.AddItem(r);
            }
        }

        //Exclusively creates a new workshop
        private void saveToolStripMenuItem_Click(object sender, EventArgs e)
        {
            FileStream output;
            string filename;
            WorkshopNameForm nameprompt = new WorkshopNameForm();

            nameprompt.ShowDialog();
            filename = nameprompt.Workshopname;
            nameprompt.Close();
            //check to make sure nameprompt exited with a valid name
            if (filename != null)
            {
                filename += ".sup";

                try
                {
                    output = new FileStream(filename,
                        FileMode.Create, FileAccess.Write);
                    output.Close();
                }
                catch(System.NotSupportedException)
                {
                    MessageBox.Show("File name cann" +
                        "ot contain \\ / : * ? \" < > or | ",
                        "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
                



            }
        }

        //deletes a supply item
        private void deleteToolStripMenuItem_Click(object sender, EventArgs e)
        {
            WorkshopForm active = ActiveMdiChild as WorkshopForm;
            active.DelItem();
        }

        //opens an about message
        private void aboutToolStripMenuItem_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Workshop Supply Manager MDI\n" +
                "created by: David McGinn","About", MessageBoxButtons.OK,
                MessageBoxIcon.Information);
        }
    }
}

```
