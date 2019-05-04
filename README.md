<p align="center">
  <img src="./public/favicon.ico" alt="w3tec" width="50" />
</p>

<h1 align="center">ReactJs Boilerplate</h1>

<p align="center">
  <b>A delightful way to building a Front-end With ReactJs.</b></br>
  </br>
  <sub>Made with ❤️ by <a href="https://github.com/codeninja0x01">Habesha Dev</a>,</sub>
</p>

<br />


## ❯ Getting Started

### Step 1: Set up the Development Environment

You need to set up your development environment before you can do anything.

Install [Node.js and NPM](https://nodejs.org/en/download/)

- on OSX use [homebrew](http://brew.sh) `brew install node`
- on Windows use [chocolatey](https://chocolatey.org/) `choco install nodejs`

### Step 2: Serve your App

Go to the project dir and start your app with this yarn script.

```bash
npm start
```

> This starts a local server using `webpack`, which will watch for any file changes and will restart the sever according to these changes.
> The server address will be displayed to you as `http://0.0.0.0:3000`.


## ❯ Project Structure

| Name                              | Description |
| --------------------------------- | ----------- |
| **node_modules/**                      | Project dependencies(which are from package.json file) are stored here. This folder might not be around until npm install command. |
| **public/**                         | This folder contains an html file which react project will work in. This is also the place if you like to add a favicon. |
| **src/**                          | This is the source of the project. |
| **src/assets/**          | This folder contains items that are related with React. Basically fonts, images and style files. You may reach this folder with Assets alias from all directories. |
| **src/components/**  | This is a place where you may find all the components used in the project. You can find additional information about contents of this folder in "Components" section of this documentation. You may reach this folder with Components alias from all directories. |
| **src/constants/** | This folder contains constants that used throughout the project. You may reach this folder with Constants alias from all directories.  |
| **src/containers/**               | This is the place where i put layout components. Top bar and menu can be found here. You may reach this folder with Containers alias from all directories. |
| **src/data/**         | i like to keep our code clean and want to separate data from logic so i put all the data used throughout the project here as json files. You may reach this folder with Data alias from all directories.. |
| **src/lang/**          |This is the folder for language files.s |
| **src/redux/**               | This is the place where redux code is. Every component that uses redux has a folder here which might contain action.js reducer.js and saga.js files. The files at the route of this folder contains code for store connection for components that uses redux. You may reach this folder with Redux alias from all directories. |
| **src/routes/**         |This is the folder where pages of the project can be found. Index.js file in this folder is responsible for parent page route defining. Every folder under this directory also has an index.js file which has a duty to define routes for sub pages. Files beside index.js are the pages of the project. You may reach this folder with Routes alias from all directories. |
| **src/util/**             |Utilities that used throughout the project is located here. You may reach this folder with Utils alias from all directories. |

## ❯ Adding Menu Item to Sidebar

Menu has a two basic item that one is for "parent" and other one is "subpage"

If your page needs to be under a parent page here is what needs to be done at src/containers/Sidebar/index.js file:

Please locate the following code block. This is where the main navigation starts.
```html
<div className="sidebar">
    <div className="main-menu">
        <div className="scroll" >
            <PerfectScrollbar>
                <Nav vertical className="list-unstyled">
```

Under Nav tag you should add new NavItem which is named new-main-menu as an example.

```html
<NavItem className={classnames({ "active": this.state.selectedParentMenu == 'new-main-menu' })}>
    <NavLink to="/app/new-main-menu" onClick={(e) => this.openSubMenu(e, 'new-main-menu')}>
        <i className="simple-icon-control-play" /> 
        <IntlMessages id="menu.new-main-menu" />
    </NavLink>
</NavItem>
```
To declare sub menu items you need to locate following codeblock


```html
<div className="sub-menu">
    <div className="scroll">
        <PerfectScrollbar>
```
Here you need to create a Nav item which is named new-main-menu-sub-item as an example.
```html
<Nav className={classnames({ "d-block": this.state.selectedParentMenu == 'new-main-menu' })} data-parent="new-main-menu">
    <NavItem>
        <NavLink to="/app/new-main-menu/new-main-menu-sub-item">
            <i className="simple-icon-shuffle" />
            <IntlMessages id="menu.default" />
        </NavLink>
    </NavItem>
</Nav>
```
If your page does not contain subpages here is what needs to be done at src/containers/Sidebar/index.js file:

Please locate the following code block. This is where the main navigation starts.

```html
<div className="sidebar">
<div className="main-menu">
    <div className="scroll" >
        <PerfectScrollbar>
            <Nav vertical className="list-unstyled">
```
Under Nav tag you should add new NavItem which is named new-main-menu-single as an example.
```html
<NavItem className={classnames({ "active": this.state.selectedParentMenu == 'new-main-menu-single' })}>
    <NavLink to="/app/new-main-menu-single">
        <i className="simple-icon-control-play" /> 
        <IntlMessages id="menu.new-main-menu-single" />
    </NavLink>
</NavItem>
```

## ❯ Adding Menu Labels To Language File

To add new-main-menu label to lang file you need to locate src/Lang/locales/en_US.js file and add this code under module.exports
```json
"menu.new-main-menu" :"Your Label of Choice"
```
If you want the breadcrumb work automatically, you need to have same ids as your page paths.
Let's say you have a page with following url: "/app/first-menu/first-sub-menu". To make breadcrumb work lang file should contain all of the 3 items in the url

```javascript
module.exports = {
    “menu.app" : “Home",
    “menu.new-main-menu" :"New Main Menu Text",
    “menu.new-main-menu-sub-item" :"New Main Menu Sub Item Text"
}
```

## ❯ Creating the Page

When you have a new-main-menu parent and new-main-menu-sub-item sub page item, you should create a folder under src/routes named as new-main-menu.
Then you should add an index.js file under this folder.
For subpage you need to add a file under this folder named new-main-menu-sub-item.js

After adding these files and folders some changes needs to be done under src/routes/index.js file. A new Route should be added under Switch tag.

```XML
<Switch>
    <Route path={`${match.url}/new-main-menu`} component={newMainMenuRoute} />
    <Route...
    <Route...
    <Route...
</Switch>
```
If your parent does not have a sub page you may insert your content under src/routes/new-main-menu/index.js file.

If it has sub page then the index.js file should point the sub pages like this:

```xml
<Switch>
    <Redirect exact from={`${match.url}/`} to={`${match.url}/new-main-menu-sub-item`} />
    <Route path={`${match.url}/new-main-menu-sub-item`} component={newMainMenuSubComponent } />
    <Route...
    <Route...
    <Route...
</Switch>
```
