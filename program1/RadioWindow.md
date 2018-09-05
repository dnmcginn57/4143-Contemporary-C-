```csharp
//David McGinn
//9-5-18
//Making a non-functional gui for a radio app

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace RadioApp
{
    public partial class RadioWindow : Form
    {
        public RadioWindow()
        {
            InitializeComponent();
        }

        //I wanted to make it so the x closed the program, just for fun
        private void textBox2_TextChanged(object sender, EventArgs e)
        {
            Application.Exit();
        }
    }
}

```
