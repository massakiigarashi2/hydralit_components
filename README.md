# **Hydralit Components** <img src="https://github.com/TangleSpace/hydralit/raw/main/docs/images/hydra.png" alt="hydra" width="50"/>
A package of Streamlit components that can be used directly or with the [Hydralit](https://github.com/TangleSpace/hydralit) library.

## **Current Components**
 - ### **Navbar**
 - ### **Loaders**
 - ### **Experimental**

<br>
<p align="center">
	<a href="https://pepy.tech/project/hydralit_components/" alt="PyPI downloads">
	<img src="https://pepy.tech/badge/hydralit_components" />
	</a>
    <a href="https://www.python.org/" alt="Python version">
        <img src="https://img.shields.io/pypi/pyversions/hydralit_components" /></a>
    <a href="https://pypi.org/project/hydralit_components/" alt="PyPI version">
        <img src="https://img.shields.io/pypi/v/hydralit_components" /></a>
    <a href="https://hydralit_components.aur-license.org/" alt="License">
        <img src="http://img.shields.io/:license-Apache-blue.svg?style=flat-square"></a>
    <a href="https://streamlit.io/" alt="Streamlit">
        <img src="http://img.shields.io/:streamlit->=0.67.0-blue.svg?style=flat-square"></a>
</p>

## Installing Hydralit Components
Hydralit can be installed from PyPI:

```bash
pip install -U hydralit_components
```
# New in version 1.0.6 (navbar updates)
NOTE: Since everyone complained about the "jumping navbar", it is now pinned to the top of the page, it is no longer sticky. If you want a sticky, non-jumping, with the Streamlit hamburger navbar all in one magical solution, keep asking Streamlit, since they have already stated they are looking to implement this feature themselves and Hydralit and Hydralit Components can go F^%& itself according to the way I've been treated by the Streamlit team. So if you have any issues with the way the navbar works, raise an issue or talk to Streamlit.
<br><br>
You can have jumpy navbar that is sticky, or non-jumping navbar that is pinned to the top, ask Streamlit for both.

 - Changed the sticky behaviour (if you want it at the top, like Streamlit ordering, declare it first) NOTE: The `sticky_nav` parameter moves the navbar to the top of the window, use `sticky_mode = 'sticky'` or `sticky_mode = 'pinned'` if you want it to be sticky, but it will be jumpy or pinned and not jumpy. If you want the Streamlit hamburger menu to appear with the navbar use `hide_streamlit_markers=False`
 - Can co-exist with the Streamlit hamburger menu now, as well as the status indicators (running/stop..)
 - Improved the centering and appearance
 - Can toggle the Streamlit markers on/off independantly of the sticky nav setting
 - Bug fix with intial value with label and id provided (Thanks [Daveography](https://github.com/Daveography)!)

# New in version 1.0.5
 - Can toggle navbar animation on/off
 - Tighten up the navbar animation
 - Add over 20 custom loaders that work the same as the built-in spinner
 - An ability to enable experimental features to allow for previously disallowed code injection (like javascript)
 - Added a modified version of the existing Streamlit cookie manager to allow for better use in multi-app environments

# New in version 1.0.3
 - Enable sticky menu mode (pin to top of the window)
 - Animated dropdown menu entries to support complex navigation
 - Offline support
 - Added support for fontawesome icons
 - Full collapse in mobile view (the burger is back!)

# Features
 - Full theme color support
 - Full container support (can put on sidebar too)
 - Responsive layout
 - Use Bootstrap icons or emojis or nothing
 - Configure Response values when clicked
 - Assign tooltips

# Navbar Demo
<p align="center">
<img src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/new_navbar.gif?raw=true" title="Navbar" alt="Navbar", width="100%" height="100%">
</p>

 # Navbar Modes
 ## Pinned Mode
<p align="center">
<img src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/pinned_nav_new.gif?raw=true" title="Navbar" alt="Navbar", width="100%" height="100%">
</p>

 ## Sticky (jumpy) Mode
<p align="center">
<img src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/sticky_nav_new?raw=true" title="Navbar" alt="Navbar", width="100%" height="100%">
</p>

 ## Regular Mode
<p align="center">
<img src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/non-sticky_nav_new.gif?raw=true" title="Navbar" alt="Navbar", width="100%" height="100%">
</p>


A very quick example of how to modify the menu items and to show we can put it on the main page, sidebar or within a container, up to you.
```python
import streamlit as st
import hydralit_components as hc


st.set_page_config(layout='wide',initial_sidebar_state='collapsed',)

# specify the primary menu definition
menu_data = [
    {'icon': "far fa-copy", 'label':"Left End"},
    {'id':'Copy','icon':"🐙",'label':"Copy"},
    {'icon': "far fa-chart-bar", 'label':"Chart"},#no tooltip message
    {'icon': "far fa-address-book", 'label':"Book"},
    {'id':' Crazy return value 💀','icon': "💀", 'label':"Calendar"},
    {'icon': "far fa-clone", 'label':"Component"},
    {'icon': "fas fa-tachometer-alt", 'label':"Dashboard",'ttip':"I'm the Dashboard tooltip!"}, #can add a tooltip message
    {'icon': "far fa-copy", 'label':"Right End"},
]


menu_id = hc.nav_bar(menu_definition=menu_data)

#get the id of the menu item clicked
st.info(f"{menu_id}")
```

 # HyLoader
<p align="center">
<img src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/standard_loaders.gif?raw=true" title="HyLoaders" alt="HyLoaders", width="45%" height="45%">
<img src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/pretty_loaders.gif?raw=true" title="HyLoaderspretty" alt="HyLoaders", width="45%" height="45%">
<img src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/pulse_bars.gif?raw=true" title="HyLoaderspretty" alt="HyLoaders", width="100%" height="60%">



A very quick example of how to use the load to wrap your long running code

```python
import hydralit_components as hc
import time

# a dedicated single loader 
with hc.HyLoader('Now doing loading',hc.Loaders.pulse_bars,):
    time.sleep(5)

# for 3 loaders from the standard loader group
with hc.HyLoader('Now doing loading',hc.Loaders.standard_loaders,index=[3,0,5]):
    time.sleep(5)

# for 1 (index=5) from the standard loader group
with hc.HyLoader('Now doing loading',hc.Loaders.standard_loaders,index=5):
    time.sleep(5)

# for 4 replications of the same loader (index=2) from the standard loader group
with hc.HyLoader('Now doing loading',hc.Loaders.standard_loaders,index=[2,2,2,2]):
    time.sleep(5)
```

 # Experimental
<p align="center">
<video controls
    src="https://github.com/TangleSpace/hydralit_components/blob/main/resources/hydrali%20experimental.mp4"
    width="800px"
    >

</video>


An example of injecting code into the Streamlit application that previously would not have worked. 
## NOTE: You need to force reload (browser refresh) the entire page after the experiemntal features have been enabled (you will see a notification in the terminal) to ensure the additions have been loaded into the web page.

```python
import hydralit_components as hc
import streamlit as st


hc.hydralit_experimental(True)


modal_code = """
<div>
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
Hydralit Components Experimental Demo!
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
<div class="modal-dialog" role="document">
<div class="modal-content">
<div class="modal-header">
  <h5 class="modal-title" id="exampleModalLabel">Modal Popup Form!</h5>
  <button type="button" class="close" data-dismiss="modal" aria-label="Close">
    <span aria-hidden="true">&times;</span>
  </button>
</div>
<div class="modal-body">
  <div class="container">
<h2>Pure JS+HTML Form</h2>
<form class="form-horizontal" action="/">
<div class="form-group">
<label class="control-label col-sm-2" for="email">Email:</label>
<div class="col-sm-10">
  <input type="email" class="form-control" id="email" placeholder="Enter email" name="email">
</div>
</div>
<div class="form-group">
<label class="control-label col-sm-2" for="pwd">Password:</label>
<div class="col-sm-10">          
  <input type="password" class="form-control" id="pwd" placeholder="Enter password" name="pwd">
</div>
</div>
<div class="form-group">        
<div class="col-sm-offset-2 col-sm-10">
  <div class="checkbox">
    <label><input type="checkbox" name="remember"> Remember me</label>
  </div>
</div>
</div>
<div class="form-group">        
<div class="col-sm-offset-2 col-sm-10">
  <button type="submit" class="btn btn-default">Submit</button>
</div>
</div>
</form>
</div>
</div>
<div class="modal-footer">
  <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
  <button type="button" class="btn btn-primary">Save changes</button>
</div>
</div>
</div>
</div>
</div>
"""


st.markdown(modal_code,unsafe_allow_html=True)
query_param = st.experimental_get_query_params()

if query_param:
    st.write('We caputred these values from the experimental modal form using Javascript + HTML + Streamlit + Hydralit Components.')
    st.write(query_param)

```

