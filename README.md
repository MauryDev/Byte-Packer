# Byte-Packer

## Support
| Tipos |
| ------------------- |
| Array |
| Dictionary |
| Numbers |
| List |
| Struct and Class (using Attribute BPObject) |
| String |
| Char |
| Boolean |
| Enum |
| DateTime |

## Examples

- Serialzie Array
```cs
static void Main(string[] args)
{
  var myarray = new byte[,] { {2,3 }, {3,4 } };
  var result = BytePackerConvert.SerializeObject(myarray);
  Console.WriteLine(result);
  // 02 00 00 00 02 00 00 00 04 00 00 00 02 03 03 04
  Console.ReadKey();
}
```

- Deserialize Number
```cs
static void Main(string[] args)
{
  var bp = new MauryDev.BytePacker.Common.BytePacker(new byte[] { 1,0,0,0});
  var result = BytePackerConvert.DeserializeObject<int>(bp);
  Console.WriteLine(result);
  // 1
  Console.ReadKey();
}
```
