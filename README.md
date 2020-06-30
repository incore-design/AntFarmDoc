<a href="https://incore.design/antfarm.html">
  <img src="https://incore.design/images/AntFarm_2048.png" title="AntFarm" alt="AntFarm" width="200" target="_blank">
</a>

## AntFarm

AntFarm is a <a href="https://www.rhino3d.com/" target="_blank">Rhino 3D</a> plugin written in C#. It permits user to store any type of data on a rhino object by storing the data on the geoemtrical object and in an in-memory SQLite database. Any operation is implemented as a Rhino commands, but can also be accessed through an UI. It also provides an API and a plugin system.

---

## Table of Contents

- [Installation](#installation)
- [Data Structure](#data-structure)
- [Rhino Commands](#rhino-commands)
- [API](#api)
- [Plugins](#plugins)
- [CopyRight](#copyright)

---

### Installation

Text how to install AntFarm and the plugins.

---

### Data Structure

AntFarm data is held in DataSets and in addition in a record on the Rhino Object. The DataSet can have Attributes.

<table>
  <tr>
    <th nowrap>Data Object</th>
    <th nowrap style="text-align: left;">Description</th>
  </tr>
  <tr>
    <td valign="top" id="dataset">DataSet</td>
    <td>
      <p>An AntFarm DataSet is represented as an in-memory data table. AntFarm is developed using an SQLite database. A DataSet can hold additional data specified in the attributes. The data not only gets stored in the database but also in the custom user data of the referenced Rhino object. A DataSet must be of unique name and can have the settings.</p>
      <b>Name</b> - AntFarm DataSet names are not case sensitive and must be unique.
      <br />
      <b>Settings</b>
      <ul>
        <li>Filter - Rhino <a href="https://developer.rhino3d.com/api/RhinoCommon/html/T_Rhino_DocObjects_ObjectType.htm" target="_blank">Object Type</a> Filter which defines the type of geometry object to be referenced in the DataSet.</li>
        <li>Colour - AntFarm <a href="#dataset">DataSet</a> colour</li>
        </ul>
    </td>
  </tr>  
  <tr>
    <td valign="top" id="attribute">Attribute</td>
    <td>
      <p>AntFarm <a href="#dataset">DataSet</a>s can hold additional data in Attributes (<a href="#dataset">DataSet</a> columns).</p>
      <b>Name</b> - AntFarm <a href="#dataset">DataSet</a> Attribute names are not case sensitive and must be unique.
      <br />
      <b id="attribute_type">Attribute Type</b>
      <ul>
        <li>Boolean - base data type</li>  
        <li><a href="#category">Category</a> - AntFarm specific data type</li>  
        <li>DateTime - base data type</li>  
        <li>Double - base data type</li>  
        <li>Float - base data type</li>  
        <li><a href="#geometric">Geometric</a> - AntFarm specific data type</li>  
        <li>Integer - base data type</li>  
        <li>String - base data type</li>  
      </ul>
    </td>
  </tr>
  <tr>
    <td valign="top" id="category">Category</td>
    <td>
      <p>AntFarm Category is a custom data type that can hold <a href="category_element">AntFarm Category Element</a>s.</p>
      <b>Name</b> - AntFarm Category names are not case sensitive and must be unique.
    </td>
  </tr>
  <tr>
    <td valign="top" id="category_element">Category Element</td>
    <td>
      <p>An AntFarm Category Element is a value in an AntFarm <a href="#category">Category</a>. An AntFarm Category ELement can hold predefined <a href="#category_element_property">AntFarm Category Element Properties</a>.</p>
      <b>Name</b> - AntFarm Category Element names are not case sensitive and must be unique.
    </td>
  </tr>
  <tr>
    <td valign="top" id="category_element_property">Category Element Property</td>
    <td>
      <p>An AntFarm Category Element Property can hold additional data on an <a href="category_element">AntFarm Category Element</a>.</p>
      <b>Name</b> - AntFarm Category Element Property names are not case sensitive and must be unique.
      <br />
      <b><a href="#property_type">Property Type</a></b> - <a href="#property_type">AntFarm Property Type</a> are AntFarm specific data types.
      <br />
      <b>Value</b> - A value based on the <a href="#property_type">AntFarm Property Type</a>.
    </td>
  </tr>
  <tr>
    <td valign="top" id="property_type">Property Type</td>
    <td>
      <p>An AntFarm Category Element Property can hold additional data on an <a href="category_element">AntFarm Category Element</a>.</p>
      <b>Name</b> - AntFarm Property Type names are not case sensitive and must be unique.
      <br />
      <b>Base Types</b>
      <ul>
        <li>Boolean - base data type</li>  
        <li><a href="#colour">Colour</a> - AntFarm specific data type</li>  
        <li>DateTime - base data type</li>  
        <li>Double - base data type</li>
        <li>Integer - base data type</li>  
        <li>String - base data type</li>  
      </ul>
    </td>
  </tr>
  <tr>
    <td valign="top" id="geometric">Geometric</td>
    <td>
      <p>An AntFarm specific data type that exposes geometrical data evaluated on the Rhino Object.</p>
      <b>Supported Types</b>
      <ul>
        <li>None - base data type</li>  
        <li>Length - evaluates the length of an object if property is supported</li>  
        <li>Area - evaluates the area of an object if property is supported</li>  
        <li>Volume - evaluates the Volume of an object if property is supported</li>  
        <li>X_Value - evaluates the x-coordinate of an object if property is supported</li>  
        <li>Y_Value - evaluates the x-coordinate of an object if property is supported</li>  
        <li>Z_Value - evaluates the x-coordinate of an object if property is supported</li>  
      </ul>
    </td>
  </tr>
  <tr>
    <td valign="top" id="colour">Colour</td>
    <td>
      <p>An AntFarm Category Element Property can hold additional data on an <a href="category_element">AntFarm Category Element</a>.</p>
      <b>A</b> - Transparency value of type byte.
      <br />
      <b>R</b> - Red value of type byte.
      <br />
      <b>G</b> - Green value of type byte.
      <br />
      <b>B</b> - Blue value of type byte.
    </td>
  </tr>
</table>

### Rhino Commands

<table>
<tr>
<td><b>Command</b></td>
<td><b>Description</b></td>
</tr>
<tr>
<td colspan="2">General Commands</td>
</tr>
<tr>
<td valign="top">AntFarm</td>
<td valign="top">Opens the main AntFarm dockable panel.</td>
</tr>
<tr>
<td valign="top">AF_Settings</td>
<td valign="top">Opens the AntFarm settings dialog.</td>
</tr>
<tr>
<td colspan="2">Commands related to <a href="#dataset">DataSet</a>s.</td>
</tr>
<tr>
<td valign="top">AF_DataSetAddTo</td>
<td valign="top">Adds Rhino objects to a <a href="#dataset">DataSet</a>. This allows the user to store additional data on a Rhino object.
<br/><br/>Command line options:
<ul>
<li><b>DataSet</b> - Name of <a href="#dataset">DataSet</a> to add to</li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_DataSetChangeColor</td>
<td valign="top">Allows for changing the <a href="#dataset">DataSet</a> color.</td>
</tr>
<tr>
<td valign="top">AF_DataSetClose</td>
<td valign="top">Close a displayed <a href="#dataset">DataSet</a> (default: current selected <a href="#dataset">DataSet</a>). Removes <a href="#dataset">DataSet</a> display from tabcontrol.</td>
</tr>
<tr>
<td valign="top">AF_DataSetCloseAll</td>
<td valign="top">Close all displayed <a href="#dataset">DataSet</a>s. Remove all <a href="#dataset">DataSet</a>s from tabcontrol.</td>
</tr>
<tr>
<td valign="top">AF_DataSetCloseAllButThis</td>
<td valign="top">Close all displayed <a href="#dataset">DataSet</a>s but the current selected.</td>
</tr>
<tr>
<td valign="top">AF_DataSetCSVExport</td>
<td valign="top">Exports the data of an AntFarm <a href="#dataset">DataSet</a> to csv file.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to export</td>
    </tr>
    <tr>
      <td valign="top"><b>Browse</b></td>
      <td valign="top">Opens a file dialog to specify file to export to</td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_DataSetCSVImport</td>
<td valign="top">Imports data from a csv file to an AntFarm <a href="#dataset">DataSet</a>.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to export</td>
    </tr>
    <tr>
      <td valign="top"><b>Browse</b></td>
      <td valign="top">Opens a file dialog to specify file to export to</td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_DataSetDelete</td>
<td valign="top">Delete a <a href="#dataset">DataSet</a> and its related data. Allows for deleting associated rhino objects.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to export</td>
    </tr>
    <tr>
      <td valign="top"><b>Yes</b></td>
      <td valign="top">All Rhino objects will get deleted. If rhino objects exist in other <a href="#dataset">DataSet</a>s entries will also get removed from other <a href="#dataset">DataSet</a>s</td>
    </tr>
    <tr>
      <td valign="top"><b>No</b></td>
      <td valign="top">Rhino objects keep existing, but AntFarm data will get removed from the objects.</td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_DataSetNew</td>
<td valign="top">Creates a new <a href="#dataset">DataSet</a> in AntFarm with in-memory data element and <a href="https://www.sqlite.org" target="_blank">SQLite</a> table.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> (names respect case-sensitive spelling and must be alphanumeric)</td>
    </tr>
    <tr>
      <td valign="top"><b>Filter</b></td>
      <td valign="top">Rhino objects filter based on <a href="http://developer.rhino3d.com/api/RhinoCommon/html/T_Rhino_DocObjects_ObjectType.htm" target="_blank">Rhino ObjectType</a></td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_DataSetOpen</td>
<td valign="top">Opens an existing before closed dataset from the <a href="https://www.sqlite.org/" target="_blank">SQLite</a> in-memory database and adds it to the tab control.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> (names respect case-sensitive spelling and must be alphanumeric)</td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_DataSetRemoveFrom</td>
<td valign="top">Removes a Rhino object from a <a href="#dataset">DataSet</a>.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to remove Rhino geometry objects from.</td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_DataSetRename</td>
<td valign="top">Rename an existing <a href="#dataset">DataSet</a> (default: current selected <a href="#dataset">DataSet</a>).
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to rename.</td>
    </tr>
  </table></td>
</tr>
<tr>
<td colspan="2">Commands related to <a href="#attribute">Attribute</a>s.</td>
</tr>
<tr>
<td valign="top">AF_AttributeAdd</td>
<td valign="top">Adds a new <a href="#attribute">Attribute</a> (Column) to the <a href="#dataset">DataSet</a>.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to add the <a href="#attribute">Attribute</a>.</td>
    </tr>
    <tr>
      <td valign="top"><b>Type</b></td>
      <td valign="top"><a href="#attribute_type">Type</a> of <a href="#attribute">Attribute</a>.</td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_AttributeMove</td>
<td valign="top">Not supported.</td>
</tr>
<tr>
<td valign="top">AF_AttributeRename</td>
<td valign="top">Rename an existing <a href="#attribute">Attribute</a>.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> that holds the <a href="#attribute">Attribute</a>.</td>
    </tr>
    <tr>
      <td valign="top"><b>Attribute</b></td>
      <td valign="top">Name of the <a href="#attribute">Attribute</a> to be renamed.</td>
    </tr>
  </table></td>
</tr>
<tr>
<td valign="top">AF_AttributeRemove</td>
<td valign="top">Removes an <a href="#attribute">Attribute</a> from a <a href="#dataset">DataSet</a> and removes the associated data from the Rhino object.
  <br />
  Command line options:
  <table>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> that holds the <a href="#attribute">Attribute</a>.</td>
    </tr>
    <tr>
      <td valign="top"><b>Attribute</b></td>
      <td valign="top">Name of the <a href="#attribute">Attribute</a> to be removed.</td>
    </tr>
  </table></td>
</tr>
</table>

### API

---

### Plugins

---

### CopyRight

<!-- [![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)** -->
- Copyright 2020 © <a href="https://incore.design" target="_blank">InCore Design</a>.
