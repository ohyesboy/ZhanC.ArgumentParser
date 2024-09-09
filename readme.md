Parse the arguments from console

```c#
var reader = new ConsoleArgumentParser(typeof(TargetType), true);
var args = new string[] { "NamelessParameter1",
        "-StringProperty", "Value1",
        "-StringPropertyWithDescription", "Value2",
        "-IntegerProperty", "3",
        "-NullableIntegerProperty", "4",
        "-NullableIntegerPropertyWithDefault", "5",
        "-NullableIntegerPropertyRequired", "6",
        "-BoolProperty", //bool flag alone
        "-BoolProperty2", //bool flag with True
        "True",
        "-BoolProperty3", //bool flag with False
        "false",
        "NamelessParameter2"};

var actual = reader.ReadArguments<TargetType>(args);
Assert.Equal("Value1", actual.StringProperty);
Assert.Equal("Value2", actual.StringPropertyWithDescription);
Assert.Equal(3, actual.IntegerProperty);
Assert.Equal(4, actual.NullableIntegerProperty);
Assert.Equal(5, actual.NullableIntegerPropertyWithDefault);
Assert.Equal(6, actual.NullableIntegerPropertyRequired);
Assert.True(actual.BoolProperty);
Assert.True(actual.BoolProperty2);
Assert.Equal("NamelessParameter1", reader.ValueArguments[0]);
Assert.Equal("NamelessParameter2", reader.ValueArguments[1]);
Assert.Null(reader.Error);


public class TargetType
{
    [CmdLineArgument]
    public string? StringProperty { get; set; }

    [CmdLineArgument(Default = "This is cool")]
    public string? StringPropertyWithDefault { get; set; }

    [CmdLineArgument(Description = "This is also cool")]
    public string? StringPropertyWithDescription { get; set; }

    [CmdLineArgument]
    public int IntegerProperty { get; set; }

    [CmdLineArgument]
    public int? NullableIntegerProperty { get; set; }

    [CmdLineArgument(Default = -1000)]
    public int? NullableIntegerPropertyWithDefault { get; set; }

    [CmdLineArgument(IsRequired = true)]
    public int? NullableIntegerPropertyRequired { get; set; }

    [CmdLineArgument]
    public bool BoolProperty { get; set; }

    [CmdLineArgument]
    public bool BoolProperty2 { get; set; }

    [CmdLineArgument]
    public bool BoolProperty3 { get; set; }

    [CmdLineArgument(Default = true)]
    public bool BoolPropertyWithDefault { get; set; }
}
```

