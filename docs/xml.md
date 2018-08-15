
# XML Functionality

This page documents the XML functionality available in noxDB. Header file: `headers/XMLPARSER.rpgle`.

---

## xml_ParseFile

```
Pointer xml_ParseFile( String path : [String options] )
```

##### Parameters

1. Path relavtive to the current directory.
2. Options for the parser. For example: `syntax=LOOSE` is a valid parameter.

Returns Pointer to created node.

---

## xml_Error

```
Ind xml_Error( Pointer node )
```

##### Parameters

1. Pointer to node created by another XML function.

Returns `*ON` if there was an error.

##### Example

```
pXml = xml_ParseFile('./test/documents/XmlSample1.xml');

If Xml_Error(pXml) ;
  //Do thing
Endif;

xml_Close(pXml);
```

---

## xml_Message

```
Varchar(1024) xml_Message( Pointer node )
```

#### Parameters

1. Pointer to node created by other another XML function.

Returns error message create by another XML function.

---

## xml_Locate

```
Pointer xml_Locate( Pointer node : String nodepath )
```

#### Parameters

1. Pointer to node created by other another XML function.
2. Document path which points another node.

Returns Pointer to chosen document node.

#### Example

```
pXml = xml_ParseFile('./test/documents/XmlSample.xml');
pElem = xml_Locate(pXml:'/MyRoot/MyElement');

MyElem = xml_GetValueStr(pElem : 'N/A');

xml_Close(pXml);
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Myroot>
    <Myelement Myattribute1="My Company name">
   	    abc
    </Myelement>
</Myroot>
```

---

## xml_GetNext

```
Pointer xml_GetNext( Pointer node )
```

#### Parameters

1. Pointer to existing node

Returns next node in current block.

#### Example

```
pXml = xml_ParseFile('./test/documents/XmlSample.xml');
pElem = xml_locate(pXml:'/MyRoot/MyElement');

dow (pElem <> *NULL);
  MyElem   = xml_GetValueStr (pElem : 'N/A');
  MyString = xml_GetAttr     (pElem : 'MyAttribute1' : 'N/A');

  pElem = xml_GetNext(pElem);
enddo;

xml_Close(pXml);
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Myroot>
    <Myelement Myattribute1="First attr">
   	    abc
    </Myelement>
    <Myelement Myattribute1="Second attr">
   	    def
    </Myelement>
</Myroot>
```

---

## xml_GetValue

*Deprecated*: use `xml_GetValueStr` instead.

```
Varchar(32767) xml_GetValue( Pointer node : [String relativeNode] : [String defaultvalue] )
```

#### Parameters

1. Pointer to existing node
2. Relative path to node
3. Default value if not node value is found.

#### Example

```
charResult = xml_GetValue (pXml : '/Myroot/Myelement':'null');
```

---

## xml_GetValueStr

```
Varchar(32767) xml_GetValueStr( Pointer node : [String defaultvalue] )
```

#### Parameters

1. Pointer to existing node
2. Default value if not node value is found.

---

## xml_GetValueNum

```
Packed(30:15) xml_GetValueNum( Pointer node : [Packed(30:15) defaultvalue] )
```

#### Parameters

1. Pointer to existing node
2. Default value if not node value is found.

---

## xml_GetValueInt

```
Int(20) xml_GetValueNum( Pointer node : [Int(20) defaultvalue] )
```

#### Parameters

1. Pointer to existing node
2. Default value if not node value is found.

---

## xml_GetAttr

*Deprecated*: use `xml_GetNodeAttrValue` instead.

```
Varchar(32767) xml_GetElemValue( Pointer node : String attrname : [String defaultvalue] )
```

#### Parameters

1. Pointer to existing node
2. Attribute name on chosen node.
2. Default value if not attribute is found.

---

## xml_GetNodeAttrValue

```
Varchar(32767) xml_GetNodeAttrValue( Pointer node : String attrname : [String defaultvalue] )
```

#### Parameters

1. Pointer to existing node
2. Attribute name on chosen node.
2. Default value if not attribute is found.

---

## xml_SetNodeAttrValue

Not only does this API update an existing attribute on a node, but will add the attribute if it does not exist.

```
void xml_GetNodeAttrValue( Pointer node : String attrname : String newValue )
```

#### Parameters

1. Pointer to existing node
2. Attribute name on chosen node.
2. New value for selected attribute.

---

## xml_Close

Close all nodes in this node/tree.

```
void xml_Close( Pointer node )
```

#### Parameters

1. Pointer to existing node.