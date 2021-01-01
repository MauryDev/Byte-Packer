# Byte-Packer

## Types support

| Types |
| ------------------- |
| Array |
| Dictionary |
| Numbers |
| List |
| Struct and Class (using Attribute BPObject and BPField) |
| String |
| Char |
| Boolean |
| Enum |
| DateTime |

## Examples

- Serialize Array
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
- Serialzie Struct
```cs
[BPObject]
struct Game
 {
  [BPField]
  public int level;
  [BPField]
  public int xp;
  [BPField]
  public string username;
  public override string ToString()
  {
    return "Level: " + level + " XP: "+ xp + " Username: "+username;
  }
}
static void Main(string[] args)
{
  var UserInfo = new User() { xp =2,username = "29",level = 10};
  var result = BytePackerConvert.SerializeObject(UserInfo);
  Console.WriteLine(result);
  /*
  3A 00 00 00 05 00 00 00 6C 00 65 00 76 00 65 00 6C 00 0A 00 00 00 02 00 00 00 78 00 70 00 02 00 00 00 08 00 00 00 75 00 73 00 65 00 72 00 6E 00 61 00 6D 00 65 00 02 00 00 00 32 00 39 00
  */
  Console.ReadKey();
}
```
- Deserialize Struct
```cs
[BPObject]
struct Game
 {
  [BPField]
  public int level;
  [BPField]
  public int xp;
  [BPField]
  public string username;
  public override string ToString()
  {
    return "Level: " + level + " XP: "+ xp + " Username: "+username;
  }
}
static void Main(string[] args)
{
  var UserInfo = new User() { xp =2,username = "29",level = 10};
  var bp = BytePackerConvert.SerializeObject(UserInfo);
  var value = BytePackerConvert.DeserializeObject<User>(bp);
  Console.WriteLine(value);
  // Level: 10 XP: 2 Username: 29
  Console.ReadKey();
}
```
- Encrypt BytePacker
```cs
static void Main(string[] args)
{
  var bp = BytePackerConvert.SerializeObject(232);
  File.WriteAllBytes("bin.bp",bp.Encrypt("232").ToArray());
  
  Console.ReadKey();
}
```
- Decrypt BytePacker
```cs
static void Main(string[] args)
{
  var bp = new BytePacker(File.ReadAllBytes("bin.bp"));
  var bp_decrypt = bp.Decrypt("232");
  Console.ReadKey();
}
```
