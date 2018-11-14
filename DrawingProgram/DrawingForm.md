```csharp
//David McGinn
//CMPS 4143
//11-14-18
//This program uses a graphics object to draw a picture
//  on a canvas.

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace McGinn_Drawing
{
    public partial class DrawingForm : Form
    {
        public DrawingForm()
        {
            InitializeComponent();
            Canvas.Invalidate();
            
        }

        private void Canvas_Paint(object sender, PaintEventArgs e)
        {
            Graphics g = Canvas.CreateGraphics();
            Pen p = new Pen(Color.Black);
            Point topPoint = new Point(0,0);
            Point botPoint = new Point(0, 480);

        

            String s = "David McGinn";
            

            SolidBrush sB = new SolidBrush(Color.Black);

            g.FillRectangle(sB, 0, 0, 640, 480);

            sB.Color = Color.GhostWhite;

            g.FillEllipse(sB, -30, 120, 700, 250);

            p.Color = Color.DarkRed;
            for(int i = 0; i < 26; i++)
            {
                topPoint.X = 25 * i;
                botPoint.X = topPoint.X;

                g.DrawLine(p, topPoint, botPoint);
            }


            sB.Color = Color.Black;

            g.FillEllipse(sB, 175, 100, 300, 300);

            sB.Color = Color.White;
            botPoint.X = 50;
            botPoint.Y = 410;

            g.DrawString(s, Canvas.Font, sB, botPoint);

  

        }
    }
}

```
