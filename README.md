# Unity Smart Merge Tool

Unity comes with a built-in tool that handles prefab and scene merge conflicts. The documentation on how to set it up is scarce and confusing (specially for first time git users).
This is a guide on how to set up and use the tool with Sourcetree and Git.


## Fallback merge tool set up

Download Perforce's [Helix Visual Merge Tool](https://www.perforce.com/downloads/visual-merge-tool) and install it. Unity merge tool will use it automatically.


## Git set up

**_Note: these next steps need to be done whenever you check out a repository containing a Unity project or make a new Unity project._**

1. Go to the project folder and make sure you can see the hidden files and folders, go to the **.git folder** and open the **config** file with a text editor of your choice.

2. **Add the following lines** to the file and save it:
```
[merge]
 tool = unityyamlmerge
[mergetool "unityyamlmerge"]
 trustExitCode = false
 cmd = 'C:\\Program Files\\Unity\\Hub\\Editor\\UNITY_VERSION\\Data\\Tools\\UnityYAMLMerge.exe' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
```
**_Note: replace UNITY_VERSION with the Unity version that your project is currently on._**

## Unity project set up

**_Note: these next steps need to be done whenever you make a new Unity project._**

1. Open the project in Unity, go to the top bar and select Edit and go to **Project Settings>Editor**;

2. Change the **Version Control mode to Visible Meta Files** and the **Asset Serialization mode to Force Text**, like shown in the picture. <br/>
![](images/project-settings.png)

3. If the project is already in git, commit ProjectSettings/EditorSettings.asset file.

## How to use

1. Whenever you're merging or rebasing your project and a conflict appears, right click the file that needs resolving, select "Resolve Conflicts", then select "Launch External Merge Tool".
The tool will then resolve those conflicts for you automatically. </br>
If there is a conflict that needs human input, Perforce Merge will run and show the conflicts that need resolving (don't forget to save your changes and then close). When merging using the default settings, P4Merge's left panel will show local file ("mine"), right panel will show the incoming remote version ("theirs"), and the middle panel will show the common base version.

2. After merging, open the project in Unity to ensure everything has been merged properly.

3. After checking the merge results, switch back to Sourcetree, and remove all the backup files that was created by merge tool, along with their metafiles.


### Resources
[Unity Manual - Smart Merge](https://docs.unity3d.com/Manual/SmartMerge.html) <br/>
[Reddit - How to solve scene conflicts with Unity's Smart Merge (5.1 fixes)](https://www.reddit.com/r/Unity3D/comments/39bdq5/how_to_solve_scene_conflicts_with_unitys_smart/)<br/>
[How to use Git for Unity source control?](http://stackoverflow.com/questions/18225126/how-to-use-git-for-unity-source-control)

