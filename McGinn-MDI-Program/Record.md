```csharp
//David McGinn
//11-30-18
//CMPS-4143
//This is a multi document interface that manages supplies
//  for multiple workshops at a science convention
//  Users may enter names of custom workshops
//      and manage individual supply lists for each workshop
//  this is a serializeable record object

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace McGinn_Program8_MDI
{
    [Serializable]
    public class Record
    {
        public int Quantity { get; set; }
        public double Price { get; set; }
        public string Name { get; set; }

        public Record() : this(0, 0.0, string.Empty) { }

        public Record(int quantity, double price, string name)
        {
            Quantity = quantity;
            Price = price;
            Name = name;
        }
    }
}

```
