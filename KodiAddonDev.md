# Kodi addon dev notes
0 -> base url is at of the plugin, this is basically the path. 
1 -> its a handle for addon, I am guessing its a numeric identifier sort of thing
2 -> This is for the queries and parameter, it seems its used to make the menu and stuffs

mode = args.get('mode',None) basically means obtaint the args, search for mode in it, if None is found then create the menu. 
This makes sense, its basically like a webdirectory navigation. And this logic is checking for the absense of any param, I am guessing that if len(args) == 0 might also work.

also, if our args are like ?spam=eggs&spam=eggs&quxx=spam then args would be a dictionary with 
{'spam': ['eggs','eggs'], 
 'quux':['spam']
}

`
xbmcplugin.setContent(addon_handle, 'movies') is used to tell that this is a movies type addon. Other types are files songs etc
if mode is None:
url = build_url({'mode': 'folder', 'foldername': 'Folder One'})
li = xbmcgui.ListItem('Folder One', iconImage='DefaultFolder.png')
xbmcplugin.addDirectoryItem(handle=addon_handle, url=url,
listitem=li, isFolder=True)
url = build_url({'mode': 'folder', 'foldername': 'Folder Two'})
li = xbmcgui.ListItem('Folder Two', iconImage='DefaultFolder.png')
xbmcplugin.addDirectoryItem(handle=addon_handle, url=url,
listitem=li, isFolder=True)
xbmcplugin.endOfDirectory(addon_handle)
`

lets take it one at a time. 
if mode is none basically means if you are at start of plugin, 
then url = build a url with mode as Folder and Foldername as Folder one
then list item li as xbmcgui.ListItem('Folder one', with icon image as Default Folder
and then addDirectoryItem with handle as addon_handle and url as url, list item and isFolder as True. It must be noted that isFolder=True flag tells kodi that its **not** a playable media.
endOfDirectory is basically a means to tell that this is the last item, so if you want three items you must go ahead and use addDirectory 3-1 times and endDirectory once. 
idk why it is so, but this is what is inside the tutorials. 
now next thing is imp, 
`
elif mode[0] == 'folder':
    foldername = args['foldername'][0]
     url = 'http://www.vidsplay.com/wp-content/uploads/2017/04/alligator.mp4'
     li = xbmcgui.ListItem(foldername + ' Video', iconImage='DefaultVideo.png')
     xbmcplugin.addDirectoryItem(handle=addon_handle, url=url, listitem=li)
     xbmcplugin.endOfDirectory(addon_handle)
`
 basically says that if the mode is folder then foldername=agrs['foldername'][0]
then attach a video playing url to it, and list it. 
li is used to listItem with type as video this time. 
we add the item and then 
after that we endofdirectory with addon_handle

args:= ('args:', {})                                                                                                                                                           
addon_handler =  30                                                                                                                                                                      
base_url =  plugin://plugin.video.demo1/                                                                                                                                            
 pewpewI work pewpew                                                                                                                                                     
build_url ->  ('-------------------', 'plugin://plugin.video.demo1/?mode=folder&foldername=Folder+One')                                                                               
 ('[listitem object]-->', <xbmcgui.ListItem object at 0x7f02e4a53aa8>)                                                                                                   
# Getting input in Kodi addons

`
def getusersearch(language):
     kb = xbmc.Keyboard('default', 'heading')
     kb.setDefault('Enter Search Word')
     kb.setHeading(language + 'Search')
     kb.setHiddenInput(False)
     kb.doModal()
     if (kb.isConfirmed()):
     ▏   search_term  = kb.getText()
     ▏   return(search_term)
     else:
     ▏   return
`
so this function is basically meant to start keyboar 60, then enter the default placeholder, then the heading and idk the HiddenInput part and do modal but the kb.isConfirmed basically means if keyboard entry is confirmed (that is clicking on the done)
if yesm the search_term is assigned with the text obtained from keyboard and returned eelse nothing is done
doModal is for password type entry

