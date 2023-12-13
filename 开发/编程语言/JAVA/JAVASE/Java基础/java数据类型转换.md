# String 
## -->int
- int i = Integer.parseInt(String);

## -->short
- short i = Short.parseShort(String); 

## -->char
1. char i = String.charAt(index);//得到String中某一指定位置的char

2. char[] i = String.toCharArray(String);//得到包含整个String的char数组

## -->byte
- byte i = Byte.parseByte(String);

## -->boolean
- boolean i = Boolean.parseBoolean(String);

## -->float
- Float i = Float.parseFloat(String); 

## -->double
- Double i = Double.parseDouble(String);

## -->long
- long i = Long.parseLong(String); 


# (2byte)short
## -->String
- String i = String.valueOf(short);

## -->int
两个short变量做数学计算时将自动转型为int
- int i = Integer.valueOf(short);

## -->char
先转换成String，再考虑

## -->byte
//考虑ing

## -->boolean
//if，else

## -->float
- Float i = Float.valueOf(short); 

## -->double
- double i = Double.valueOf(short); 

## -->long
- long i = Long.valueOf(a);


# (4byte)int
## -->String
- String i = String.valueOf(int);

## -->short
- short i = Integer.valueof(int);

## -->char
## -->byte
## -->boolean
## -->float
## -->double
## -->long

# (2byte)char 
## -->String
- String i = String.valueOf(char);

## -->short
## -->int
## -->byte
## -->boolean
## -->float
## -->double
## -->long

# (1byte)byte
## -->String
- String i = String.valueOf(byte);

## -->short
## -->int
## -->char
## -->boolean
## -->float
## -->double
## -->long

# boolean 
## -->String
- String i = String.valueOf(boolean);

## -->short
## -->int
## -->char
## -->byte
## -->float
## -->double
## -->long

# (4byte)float 
## -->String
- String i = String.valueOf(float);

## -->short
## -->int
## -->char
## -->byte
## -->boolean
## -->double
## -->long

# (8byte)double 
## -->String
- String i = String.valueOf(double);

## -->short
## -->int
## -->char
## -->byte
## -->boolean
## -->float
## -->long

# (8byte)long
## -->String
- String i = String.valueOf(long);

## -->short
## -->int
## -->char
## -->byte
## -->boolean
## -->float
## -->double


# String[] | ArrayList<String>

```java
//String[] --> ArrayList<String>
String[] string=new String[5];
ArrayList<String> list = new ArrayList<String>();
//把数组转成集合，也就是把数组里面的数据存进集合；
Collections.addAll(list, string);

//ArrayList<String> --> String[]
ArrayList<String> list = new ArrayList<String>();
String[] string = (String[]) list.toArray();//集合转数组
```