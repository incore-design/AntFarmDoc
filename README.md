<a href="https://incore.design/antfarm.html">
  <img src="https://github.com/joel-putnam/AntFarm/blob/Master/Icons%2BImages/ant_2048.png" title="AntFarm" alt="AntFarm" width="200" target="_blank">
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

<table style="text-align: left; vertical-align: top;">
  <tr>
    <th nowrap>Data Object</th>
    <th nowrap style="text-align: left;">Description</th>
  </tr>
  <tr>
    <td nowrap>DataSet</td>
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
</table>

### Rhino Commands

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

---

### License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
- Copyright 2020 © <a href="https://incore.design" target="_blank">InCore Design</a>.
