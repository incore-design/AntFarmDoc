<a href="https://incore.design/antfarm.html" target="incore_design">
  <img src="https://incore.design/images/AntFarm_2048.png" title="AntFarm" alt="AntFarm" width="200" target="_blank">
</a>

## AntFarm

AntFarm is a <a href="https://www.rhino3d.com/" target="_blank">Rhino 3D v7</a> plugin written in C# using the <a href="https://docs.microsoft.com/en-us/dotnet/framework/" target="_blank">Mircosofts .net framework (4.8)</a>. It permits the user to store select data of several types on a rhino object and in an in-memory SQLite database through a series of new Rhino Commands that can also be accessed through a UI prodidging complete integration with the standard Rhino experience inlcuding save/open, import/export, copy/paste between files and full undo/redo integration. Additionally Antfarm provides an API and a plugin system to furthe enhance the core data model with domain specific tools and functions such as Grasshopper and GIS with many more tools in the future planned. 

Currently in <a href="https://en.wikipedia.org/wiki/Software_release_life_cycle#Beta" target="release">Beta</a> the core data model and functions are considered to be feature complete.

Core Data Model Includes:
*Serialize all data to .3dm files
*Copy and Pase objects and associated Data within and between Rhino Files

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

AntFarm and associated plugins are availabe in the <a href="https://www.rhino3d.com/features/package-manager/" target="packageManager">Package Manager</a>

---

### Data Structure

AntFarm data is held in SQL tables and keyed to Rhino geometry and objects as grouped themes of data collections called "DataSets". They are represented graphicaly in a familar excel like table view of columns(Attributes) and rows(Geometry Objects).

<table>
  <tr>
    <th nowrap>Data Object</th>
    <th nowrap style="text-align: left;">Description</th>
  </tr>
  <tr>
    <td valign="top" id="dataset">DataSet</td>
    <td>
      <p>An AntFarm <a href="#dataset">DataSet</a> is represented as a table view and stored as an in-memory data table. AntFarm is developed using SQLite and as such has a full SQL backend. A <a href="#dataset">DataSet</a> can hold additional data specified in the <a href="#attribute">Attribute</a>s. The data not only gets stored in the database but also keyed to referenced Rhino object where is serialzied and saved in the Rhino file. A <a href="#dataset">DataSet</a> must be of unique name and can have the following <a href="#dataset_settings">settings</a>.</p>
      <table>
        <tr>
          <td valign="top"><b>Name</b></td>
          <td valign="top">AntFarm DataSet names are not case sensitive and must be unique.</td>
        </tr>
        <tr>
          <td valign="top"><b id="dataset_settings">Settings</b></td>
          <td><table>
            <tr>
              <td valign="top"><b>Filter</b></td>
              <td valign="top">Rhino <a href="https://developer.rhino3d.com/api/RhinoCommon/html/T_Rhino_DocObjects_ObjectType.htm" target="_blank">Object Type</a> Filter which defines the type of geometrical object to be referenced in the DataSet.</td>
            </tr>
            <tr>
              <td valign="top"><b><a href="#colour">Colour</a></b></td>
              <td>AntFarm <a href="#dataset">DataSet</a> <a href="#colour">colour</a></td>
            </tr>
          </table></td>
        </tr>
      </table></td>
  </tr>  
  <tr>
    <td valign="top" id="attribute">Attribute</td>
    <td>
      <p>AntFarm <a href="#dataset">DataSet</a>s can hold additional data in <a href="#attribute">Attributes</a> (<a href="#dataset">DataSet</a> columns).</p>
      <table>
        <tr>
          <td valign="top"><b>Name</b></td>
          <td valign="top">AntFarm <a href="#dataset">DataSet</a> <a href="#attribute">Attribute</a> names are not case sensitive and must be unique.</td>
        </tr>
        <tr>
          <td valign="top"><b id="dataset_settings">Attribute types</b></td>
          <td><table>
            <tr>
              <td valign="top"><b>Boolean</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b><a href="#category">Category</a></b></td>
              <td valign="top">AntFarm specific data type.</td>
            </tr>
            <tr>
              <td valign="top"><b>Double</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b>Float</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b><a href="#geometric">Geometric</a></b></td>
              <td valign="top">AntFarm specific data type.</td>
            </tr>
            <tr>
              <td valign="top"><b>Integer</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b>String</b></td>
              <td valign="top">base data type</td>
            </tr>
          </table></td>
        </tr>
      </table></td>
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
      <table>
        <tr>
          <td valign="top"><b>Name</b></td>
          <td valign="top">AntFarm Category Element names are not case sensitive and must be unique.</td>
        </tr>
      </table></td>
  </tr>
  <tr>
    <td valign="top" id="category_element_property">Category Element Property</td>
    <td>
      <p>An AntFarm Category Element Property can hold additional data on an <a href="category_element">AntFarm Category Element</a>.</p>
      <table>
        <tr>
          <td valign="top"><b>Name</b></td>
          <td valign="top">AntFarm Category Element Property names are not case sensitive and must be unique.</td>
        </tr>
        <tr>
          <td valign="top"><b><a href="#property_type">Property Type</a></b></td>
          <td valign="top"><a href="#property_type">AntFarm Property Type</a> are AntFarm specific data types.</td>
        </tr>
        <tr>
          <td valign="top"><b>Value</b></td>
          <td valign="top">A value based on the <a href="#property_type">AntFarm Property Type</a>.</td>
        </tr>
      </table></td>
  </tr>
  <tr>
    <td valign="top" id="property_type">Property Type</td>
    <td>
      <p>An AntFarm Category Element Property can hold additional data on an <a href="category_element">AntFarm Category Element</a>.</p>
      <table>
        <tr>
          <td valign="top"><b>Name</b></td>
          <td valign="top">AntFarm Property Type names are not case sensitive and must be unique.</td>
        </tr>
        <tr>
          <td valign="top"><b>Base data types</b></td>
          <td><table>
            <tr>
              <td valign="top"><b>Boolean</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b><a href="#colour">Colour</a></b></td>
              <td valign="top">AntFarm specific data type.</td>
            </tr>
            <tr>
              <td valign="top"><b>DateTime</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b>Double</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b>Integer</b></td>
              <td valign="top">base data type</td>
            </tr>
            <tr>
              <td valign="top"><b>String</b></td>
              <td valign="top">base data type</td>
            </tr>
          </table></td>
        </tr>
    </table></td>
  </tr>
  <tr>
    <td valign="top" id="geometric">Geometric</td>
    <td>
      <p>An AntFarm specific data type that exposes geometrical data evaluated on the Rhino Object.</p>
      <table>
        <tr>
          <td valign="top"><b>None</b></td>
          <td valign="top">default value</td>
        </tr>
        <tr>
          <td valign="top"><b>Length</b></td>
          <td valign="top">Evaluates the length of an object if property is supported.</td>
        </tr>
        <tr>
          <td valign="top"><b>Area</b></td>
          <td valign="top">Evaluates the area of an object if property is supported.</td>
        </tr>
        <tr>
          <td valign="top"><b>Volume</b></td>
          <td valign="top">Evaluates the volume of an object if property is supported.</td>
        </tr>
        <tr>
          <td valign="top"><b>X_Value</b></td>
          <td valign="top">Evaluates the x-coordinate of an object if property is supported.</td>
        </tr>
        <tr>
          <td valign="top"><b>Y_Value</b></td>
          <td valign="top">Evaluates the y-coordinate of an object if property is supported.</td>
        </tr>
        <tr>
          <td valign="top"><b>Z_Value</b></td>
          <td valign="top">Evaluates the z-coordinate of an object if property is supported.</td>
        </tr>
      </table></td>
  </tr>
  <tr>
    <td valign="top" id="colour">Colour</td>
    <td>
      <p>An AntFarm specific data type to hold a colour value (serializable).</p>
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

---

### Rhino Commands

Any interaction with AntFarm related functionality is using Rhino commands. The provided UI is calling the same Rhino commands. 

<table>
<tr>
  <th><b>Command</b></th>
  <th><b>Description</b></th>
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
  <td valign="top">AF_SchemaExport</td>
  <td valign="top">needs work.</td>
</tr>
<tr>
  <td valign="top">AF_SchemaImport</td>
  <td valign="top">needs work.</td>
</tr>
<tr>
  <td colspan="2">Commands related to <a href="#dataset">DataSet</a>s.</td>
</tr>
<tr>
  <td valign="top">AF_DataSetAddTo</td>
  <td valign="top">
    <p>Adds Rhino objects to a <a href="#dataset">DataSet</a>. This allows the user to store additional data on a Rhino object.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>DataSet</b></td>
        <td valign="top">Name of <a href="#dataset">DataSet</a> to add to.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_DataSetChangeColor</td>
  <td valign="top"><p>Allows for changing the <a href="#dataset">DataSet</a> color.</p></td>
</tr>
<tr>
  <td valign="top">AF_DataSetClose</td>
  <td valign="top"><p>Close a displayed <a href="#dataset">DataSet</a> (default: current selected <a href="#dataset">DataSet</a>). Removes <a href="#dataset">DataSet</a> display from tabcontrol.</p></td>
</tr>
<tr>
  <td valign="top">AF_DataSetCloseAll</td>
  <td valign="top"><p>Close all displayed <a href="#dataset">DataSet</a>s. Remove all <a href="#dataset">DataSet</a>s from tabcontrol.</p></td>
</tr>
<tr>
  <td valign="top">AF_DataSetCloseAllButThis</td>
  <td valign="top"><p>Close all displayed <a href="#dataset">DataSet</a>s but the current selected.</p></td>
</tr>
<tr>
  <td valign="top">AF_DataSetCSVExport</td>
  <td valign="top"><p>Exports the data of an AntFarm <a href="#dataset">DataSet</a> to csv file.</p>
  <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to add to.</td>
    </tr>
    <tr>
      <td valign="top"><b>Browse</b></td>
      <td valign="top">Opens a file dialog to specify file to export to</td>
    </tr>
  </table></td>
</tr>
<tr>
  <td valign="top">AF_DataSetCSVImport</td>
  <td valign="top"><p>Imports data from a csv file to an AntFarm <a href="#dataset">DataSet</a>.</p>
  <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
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
  <td valign="top"><p>Delete a <a href="#dataset">DataSet</a> and its related data. Allows deleting of associated rhino objects.</p>
  <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to delete.</td>
    </tr>
    <tr>
      <td valign="top"><b>DeleteRhinoObjects</b></td>
      <td valign="top"><p><b>Yes</b> - All Rhino objects will get deleted. If rhino objects exist in other <a href="#dataset">DataSet</a>s, entries will also get removed from other <a href="#dataset">DataSet</a>s</p>
      <p><b>No</b> - Rhino objects keep existing, but AntFarm data will get removed from the objects.</p></td>
    </tr>
  </table></td>
</tr>
<tr>
  <td valign="top">AF_DataSetNew</td>
  <td valign="top"><p>Creates a new <a href="#dataset">DataSet</a> in AntFarm with in-memory data element and <a href="https://www.sqlite.org" target="_blank">SQLite</a> table.</p>
  <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
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
  <td valign="top"><p>Opens an existing before closed dataset from the <a href="https://www.sqlite.org/" target="_blank">SQLite</a> in-memory database and adds it to the tab control.</p>
  <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> (names respect case-sensitive spelling and must be alphanumeric)</td>
    </tr>
  </table></td>
</tr>
<tr>
  <td valign="top">AF_DataSetRemoveFrom</td>
  <td valign="top"><p>Removes a Rhino object from a <a href="#dataset">DataSet</a>.</p>
  <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
    <tr>
      <td valign="top"><b>DataSet</b></td>
      <td valign="top">Name of <a href="#dataset">DataSet</a> to remove Rhino geometry objects from.</td>
    </tr>
  </table></td>
</tr>
<tr>
  <td valign="top">AF_DataSetRename</td>
  <td valign="top"><p>Rename an <a href="#dataset">DataSet</a> (default: current selected <a href="#dataset">DataSet</a>).</p>
  <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
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
  <td valign="top"><p>Adds a new <a href="#attribute">Attribute</a> (Column) to the <a href="#dataset">DataSet</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
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
  <td valign="top"><p>Rename an existing <a href="#attribute">Attribute</a>.</p>
    <table>
    <tr>
      <td colspan="2" valign="top">Command options</td>
    </tr>
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
  <td valign="top"><p>Removes an <a href="#attribute">Attribute</a> from a <a href="#dataset">DataSet</a> and removes the associated data from the Rhino object.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
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
<tr>
  <td colspan="2">Commands related to <a href="#category">Categories</a>.</td>
</tr>
<tr>
  <td valign="top">AF_Categories</td>
  <td valign="top"><p>Displays the <a href="#category">Category</a> window which provides a UI interface to add <a href="#category">Categories</a>, <a href="#category_element">Category Elements</a>, <a href="#category_element_property">Category Element Properties</a> and <a href="#property_type">Property Types</a>.</p></td>
</tr>
<tr>
  <td valign="top">AF_CategoriesImport</td>
  <td valign="top"><p>Opens a file window dialog to import an AntFarmCategory (*.afc) file.</p></td>
</tr>
<tr>
  <td valign="top">AF_CategoriesExport</td>
  <td valign="top"><p>Exports all existing <a href="#category">Categories</a> including <a href="#category_element">Category Elements</a>, <a href="#category_element_property">Category Element Properties</a> and <a href="#property_type">Property Types</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Browse</b></td>
        <td valign="top">Opens a file window dialog to specify the file (*.afc) location and name.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_CategoryDelete</td>
  <td valign="top"><p>Deletes a <a href="#category">Category</a> from AntFarm. <a href="#category">Categories</a> in use can not be deleted.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> to delete.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_CategoryNew</td>
  <td valign="top"><p>Create a new <a href="#category">Category</a> in AntFarm.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Name</b></td>
        <td valign="top">Name of <a href="#category">Category</a> to create.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_CategoryRename</td>
  <td valign="top"><p>Rename a <a href="#category">Category</a> in AntFarm.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> to rename.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td colspan="2">Commands related to <a href="#category_element">Category Elements</a>.</td>
</tr>
<tr>
  <td valign="top">AF_ElementAdd</td>
  <td valign="top"><p>Adds a new <a href="#category_element">Category Elements</a> to a <a href="#category">Category</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Name</b></td>
        <td valign="top">Name of <a href="#category_element">Category Element</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> to add to the <a href="#category_element">Category Element</a>.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_ElementCopy</td>
  <td valign="top"><p>Copies a <a href="#category_element">Category Element</a> from one <a href="#category">Category</a> to another including all attached <a href="#category_element_property">Category Element Properties</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>FromCategory</b></td>
        <td valign="top">Name of <a href="#category">Category</a> to copy from.</td>
      </tr>
      <tr>
        <td valign="top"><b>ToCategory</b></td>
        <td valign="top">Name of <a href="#category">Category</a> to copy to.</td>
      </tr>
      <tr>
        <td valign="top"><b>Element</b></td>
        <td valign="top">Name of <a href="#category_element">Category Element</a> to copy.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_ElementRemove</td>
  <td valign="top"><p>Removes a <a href="#category_element">Category Element</a> from a <a href="#category">Category</a>. <a href="#category_element">Category Element</a> in use will not be removed.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> of <a href="#category_element">Category Element</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Element</b></td>
        <td valign="top">Name of <a href="#category_element">Category Element</a> to remove.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_ElementRename</td>
  <td valign="top"><p>Rename a <a href="#category_element">Category Element</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> of <a href="#category_element">Category Element</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Element</b></td>
        <td valign="top">Name of <a href="#category_element">Category Element</a> to rename.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td colspan="2">Commands related to <a href="#category_element_property">Category Element Properties</a>.</td>
</tr>
<tr>
  <td valign="top">AF_PropertyAdd</td>
  <td valign="top"><p>Adds a new <a href="#category_element_property">Category Element Property</a> to an exisiting <a href="#category_element">Category Element</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> hosting the <a href="#category">Category Element</a> to add to the <a href="#category_element_property">Category Element Property</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Element</b></td>
        <td valign="top">Name of the <a href="#category_element">Category Element</a> to add to the <a href="#category_element_property">Category Element Property</a>.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_PropertyRemove</td>
  <td valign="top"><p>Remove a <a href="#category_element_property">Category Element Property</a> from a <a href="#category_element">Category Element</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> hosting the <a href="#category">Category Element</a> to remove from the <a href="#category_element_property">Category Element Property</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Element</b></td>
        <td valign="top">Name of the <a href="#category_element">Category Element</a> to remove from the <a href="#category_element_property">Category Element Property</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Property</b></td>
        <td valign="top">Name of the <a href="#category_element_property">Category Element Property</a> to remove.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td valign="top">AF_PropertyRename</td>
  <td valign="top"><p>Rename a <a href="#category_element_property">Category Element Property</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> hosting the <a href="#category">Category Element</a> that hosts the <a href="#category_element_property">Category Element Property</a> to rename.</td>
      </tr>
      <tr>
        <td valign="top"><b>Element</b></td>
        <td valign="top">Name of the <a href="#category_element">Category Element</a> hosting the <a href="#category_element_property">Category Element Property</a> to rename.</td>
      </tr>
      <tr>
        <td valign="top"><b>Property</b></td>
        <td valign="top">Name of the <a href="#category_element_property">Category Element Property</a> to rename.</td>
      </tr>
    </table></td>
</tr>  
<tr>
  <td valign="top">AF_PropertyUpdateValue</td>
  <td valign="top"><p>Update the stored value in a <a href="#category_element_property">Category Element Property</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Category</b></td>
        <td valign="top">Name of <a href="#category">Category</a> hosting the <a href="#category">Category Element</a> that hosts the <a href="#category_element_property">Category Element Property</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Element</b></td>
        <td valign="top">Name of the <a href="#category_element">Category Element</a> hosting the <a href="#category_element_property">Category Element Property</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>Property</b></td>
        <td valign="top">Name of the <a href="#category_element_property">Category Element Property</a> to update the value.</td>
      </tr>
    </table></td>
</tr>
<tr>
  <td colspan="2">Commands related to <a href="#property_type">Property Types</a>.</td>
</tr>  
<tr>
  <td valign="top">AF_PropertyTypeDelete</td>
  <td valign="top"><p>Delete a <a href="#property_type">Property Type</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>PropertyType</b></td>
        <td valign="top">Name of <a href="#property_type">Property Type</a> to delete.</td>
      </tr>
    </table></td>
</tr>  
<tr>
  <td valign="top">AF_PropertyTypeNew</td>
  <td valign="top"><p>Create a new <a href="#property_type">Property Type</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>Name</b></td>
        <td valign="top">Name of <a href="#property_type">Property Type</a>.</td>
      </tr>
      <tr>
        <td valign="top"><b>BaseType</b></td>
        <td valign="top">Name of <a href="#property_type">Property Base Type</a>.</td>
      </tr>
    </table></td>
</tr>  
<tr>
  <td valign="top">AF_PropertyTypeRename</td>
  <td valign="top"><p>Rename a <a href="#property_type">Property Type</a>.</p>
    <table>
      <tr>
        <td colspan="2" valign="top">Command options</td>
      </tr>
      <tr>
        <td valign="top"><b>PropertyType</b></td>
        <td valign="top">Name of <a href="#property_type">Property Type</a> to rename.</td>
      </tr>
    </table></td>
</tr>
</table>

---

### API

Please refer to <a href="https://incore.design/antfarm_api/API/index.html" target="anfarm_api">AntFarm API</a> for further information.

---

### Plugins

---

### CopyRight

<!-- [![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)** -->
- Copyright 2020 © <a href="https://incore.design" target="_blank">InCore Design</a>.

---
