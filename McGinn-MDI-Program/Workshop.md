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
using System.Collections;

namespace McGinn_Program8_MDI
{
    public partial class WorkshopForm : Form
    {
        private string _file;
        private BinaryFormatter _formatter = new BinaryFormatter();
        public WorkshopForm(string file)
        {
            InitializeComponent();
            _file = file;
            


            DisplayList();

            
            WSNameLable.Text += Path.GetFileNameWithoutExtension(file);


        }

        //Accepts a reccord to add to the workshup's .sup file
        public void AddItem(Record r)
        {
            FileStream fstream = new FileStream(_file, FileMode.Append,
                FileAccess.Write);
            _formatter.Serialize(fstream, r);

            fstream.Close();

            DisplayList();
        }

        //deletes an item from the workshop's .sup file
        //the user will select from the ListBox the item to delete
        //This will delete based on name of the item, the first field
        public void DelItem()
        {
            ArrayList records = new ArrayList();
            FileStream fstream = new FileStream(_file, FileMode.Open,
                FileAccess.Read);
            int index;
            string target;

            //get the name of the record to delete
            if (ItemList.SelectedItem != null)
            {
                target = ItemList.SelectedItem.ToString();
                index = target.IndexOf('$');
                target = target.Substring(0, index);
                target = target.Replace("\t", "");
                target.TrimEnd();

                //populate array list with Records and delete the proper
                //  record
                try
                {
                    while (true)
                    {
                        Record record = (Record)_formatter.Deserialize(fstream);

                        records.Add(record);
                    }
                }
                catch (SerializationException)
                {
                }

                Record tmp = new Record();
                foreach (Record r in records)
                {
                    if (r.Name.Equals(target))
                    {
                        tmp = r;
                    }
                }
                records.Remove(tmp);

                fstream.Close();
                ReWrite(records);

            }
            else
                MessageBox.Show("You must select an item to remove",
                    "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);

        }

        //Called only by DelItem(), rewrites a list of records to the file
        //  calls additem
        private void ReWrite(ArrayList records)
        {
            //clear the contents of the supply file
            FileStream clr = new FileStream(_file, FileMode.Create,
                FileAccess.Write);
            clr.Close();
            //bool toClear = true;

            //write the new contents
            foreach(Record r in records)
            {
                AddItem(r);
            }

            DisplayList();
        }

        //displays all the items in a .sup file in alistbox
        private void DisplayList()
        {
            ItemList.Items.Clear();
            FileStream fstream = new FileStream(_file, FileMode.Open, 
                FileAccess.Read);
            string output;
            try
            {
                while (true)
                {
                    Record record = (Record)_formatter.Deserialize(fstream);

                    output = record.Name + "\t$" + record.Price + "\t" +
                        record.Quantity + Environment.NewLine;

                    ItemList.Items.Add(output);
                }
            }
            catch (SerializationException)
            {
            }
            fstream.Close();
        }

    }
}

```
