<a href="https://incore.design/antfarm.html">
  <img src="https://incore.design/images/AntFarm_2048.png" title="AntFarm" alt="AntFarm" width="200" target="_blank">
</a>

## AntFarm

AntFarm is a <a href="https://www.rhino3d.com/" target="_blank">Rhino 3D</a> plugin written in C#. It permits user to store any type of data on a rhino object by storing the data on the geoemtrical object and in an in-memory SQLite database. Any operation is implemented as a Rhino commands, but can also be accessed through an UI. It also provides an API and a plugin system.

## Table of Contents

- [Installation](#installation)
- [Data Structure](#data-structure)
- [Rhino Commands](#rhino-commands)
- [API](#api)
- [Plugins](#plugins)
- [License](#license)


---

### Installation

Text how to install AntFarm and the plugins.

### Data Structure

AntFarm data is held in DataSets and in addition in a record on the Rhino Object. The DataSet can have Attributes.

<table>
  <tr>
    <th nowrap>Data Object</th>
    <th nowrap style="text-align: left;">Description</th>
  </tr>
  <tr>
    <td nowrap valign="top" id="dataset">DataSet</td>
    <td>
      <p>An AntFarm DataSet is represented as an in-memory data table. AntFarm is developed using an SQLite database. A DataSet can hold additional data specified in the attributes. The data not only gets stored in the database but also in the custom user data of the referenced Rhino object. A DataSet must be of unique name and can have the settings.</p>
      <h4>Name</h4>
      &nbsp;&nbsp;AntFarm DataSet names are not case sensitive and must be unique.
      <h4>Settings</h4>
      <ul>
        <li>Filter - Rhino <a href="https://developer.rhino3d.com/api/RhinoCommon/html/T_Rhino_DocObjects_ObjectType.htm" target="_blank">Object Type</a> Filter which defines the type of geometry object to be referenced in the DataSet.</li>
        <li></li>
        </ul>
    </td>
  </tr>  
  <tr>
    <td nowrap valign="top" id="attribute">Attribute</td>
    <td>
      <p>Text ...</p>
      <h4>Name</h4>
      &nbsp;&nbsp;AntFarm DataSet names are not case sensitive and must be unique.
      <h4>Settings</h4>
      <ul>
        <li>Filter - Rhino <a href="https://developer.rhino3d.com/api/RhinoCommon/html/T_Rhino_DocObjects_ObjectType.htm" target="_blank">Object Type</a> Filter which defines the type of geometry object to be referenced in the DataSet.</li>
        <li></li>
        </ul>
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
<td valign="top">AF_DataSetNew</td>
<td valign="top">Creates a new <a href="#dataset">DataSet</a> in AntFarm with in-memory data element and <a href="https://www.sqlite.org" target="_blank">SQLite</a> table.
<br/><br/>Command line options:
<ul>
<li>Name (names respect case-sensitive spelling and must be alphanumeric)</li>
<li>Filter - Rhino objects filter based on <a href="http://developer.rhino3d.com/api/RhinoCommon/html/T_Rhino_DocObjects_ObjectType.htm" target="_blank">Rhino Objecttype</a></li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_DataSetChangeColor</td>
<td valign="top">Allows for changing the <a href="#dataset">DataSet</a> color.</td>
</tr>
<tr>
<td valign="top">AF_DataSetOpen</td>
<td valign="top">Opens an existing before closed dataset from the <a href="https://www.sqlite.org/" target="_blank">SQLite</a> in-memory database and adds it to the tab control.
<br/><br/>Command line options:
<ul>
<li>Name</li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_DataSetOpenAll</td>
<td valign="top">Opens all existing <a href="#dataset">DataSet</a>s from the SQLite database and adds them to the tab control.</td>
</tr>
<tr>
<td valign="top">AF_DataSetRename</td>
<td valign="top">Rename an existing <a href="#dataset">DataSet</a> (default: current selected <a href="#dataset">DataSet</a>).
<br/><br/>Command line options:
<ul>
<li>New Name (names respect case-sensitive spelling and must be alphanumeric)</li>
</ul></td>
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
<td valign="top">AF_DataSetDelete</td>
<td valign="top">Delete a <a href="#dataset">DataSet</a> and its related data. Allows for deleting associated rhino objects.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="#dataset">DataSet</a> to be deleted</li>
<li>YES - all Rhino objects will get deleted. If rhino objects exist in other <a href="#dataset">DataSet</a>s entries will also get removed from other <a href="#dataset">DataSet</a>s.</li>
<li>NO - Rhino objects keep existing, but AntFarm data will get removed from the objects.</li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_DataSetAddTo</td>
<td valign="top">Adds Rhino objects to a <a href="#dataset">DataSet</a>. This allows the user to store additional <a href="https://github.com/joel-putnam/AntFarm/wiki/data">data</a> on a Rhino object.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="#dataset">DataSet</a> to add to</li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_DataSetRemoveFrom</td>
<td valign="top">Removes a Rhino object from a <a href="#dataset">DataSet</a>.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="#dataset">DataSet</a> to remove from</li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_DataSetCSVExport</td>
<td valign="top">Exports the data of an AntFarm <a href="#dataset">DataSet</a> to csv file.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="#dataset">DataSet</a> to export</li>
<li>File location to export to</li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_DataSetCSVImport</td>
<td valign="top">Imports data from a csv file to an AntFarm <a href="#dataset">DataSet</a>.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="#dataset">DataSet</a> to import to</li>
<li>File location to of csv file</li>
</ul></td>
</tr>
<tr>
<td colspan="2">Commands related to <a href="#attribute">Attribute</a>s.</td>
</tr>
<tr>
<td valign="top">AF_AttributeNew</td>
<td valign="top">Adds a new <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">attribute</a> (Column) to the  <a href="https://github.com/joel-putnam/AntFarm/wiki/DataSet">dataset</a>.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="https://github.com/joel-putnam/AntFarm/wiki/DataSet">dataset</a> to add the <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">attribute</a> to</li>
<li><a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">Attribute type</a></li>
<li>Additional option for either <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">Attribute type</a> <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">category</a>, <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">geometric attribute</a></li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_AttributeRename</td>
<td valign="top">Rename an existing <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">attribute</a>.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="https://github.com/joel-putnam/AntFarm/wiki/DataSet">dataset</a> owning the <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">attribute</a></li>
<li>Name of <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">Attribute</a> to be renamed</li>
</ul></td>
</tr>
<tr>
<td valign="top">AF_AttributeMove</td>
<td valign="top">Move/Copy an <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">attribute</a> from one <a href="https://github.com/joel-putnam/AntFarm/wiki/DataSet">dataset</a> to another.
(not implemented, see <a href="https://github.com/joel-putnam/AntFarm/issues/46">Issue 46</a>)</td>
</tr>
<tr>
<td valign="top">AF_AttributeDelete</td>
<td valign="top">Deletes an <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">attribute</a> from a <a href="https://github.com/joel-putnam/AntFarm/wiki/DataSet">dataset</a> and removes the data from the Rhino object.
<br/><br/>Command line options:
<ul>
<li>Name of <a href="https://github.com/joel-putnam/AntFarm/wiki/DataSet">dataset</a> owning the <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">attribute</a></li>
<li>Name of <a href="https://github.com/joel-putnam/AntFarm/wiki/Attribute">Attribute</a> to be deleted</li>
</ul></td>
</tr>
</table>

---

### License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
- Copyright 2020 © <a href="https://incore.design" target="_blank">InCore Design</a>.
