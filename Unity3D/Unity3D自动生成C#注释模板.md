
# 如何Unity3D自动生成C#注释模板？


 在Unity编辑器中新建一个C#脚本的时候，Unity会调用“Unity:unity\Editor\Resources\ScriptTemplates"下“81-C#Script-NewBehaviourScript.cs.txt"文档中的模板。

只要修改一下文件，再在Unity编辑下写一个脚本就可以实现了

### 具体步骤：

1. 打开Unity:unity\Editor\Resources\ScriptTemplates下的81-C#Script-NewBehaviourScript.cs.txt
进行如下编辑，也可自定义编辑
![image](https://note.youdao.com/yws/public/resource/1a489604cd05a960727518718b82f4e4/xmlnote/80D506E5B57942F0A4DAB432106FC10C/1566)

2. 在Unity编辑器下新建Editor文件夹. </br>
![image](https://note.youdao.com/yws/public/resource/1a489604cd05a960727518718b82f4e4/xmlnote/8E5907AAEF464D98B28C572E583C54CE/1575) </br>
在Editor文件夹下新建C#脚本AddFileHeadComment.cs（.cs文件名不用写）。</br>
![image](https://note.youdao.com/yws/public/resource/1a489604cd05a960727518718b82f4e4/xmlnote/96AF320047C84DE896122BAF4ED51EC6/1577)

3. 编写AddFileHeadComment.cs脚本。

**AddFileHeadComment.cs**
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System.IO;
using UnityEditor;

public class AddFileHeadComment : UnityEditor.AssetModificationProcessor{

    public static void OnWillCreateAsset(string newFileMeta)
    {
        string newFilePath = newFileMeta.Replace(".meta", "");
        string fileExt = Path.GetExtension(newFilePath);
        if (fileExt != ".cs")
        {
            return;
        }
        //注意，Application.datapath会根据使用平台不同而不同  
        string realPath = Application.dataPath.Replace("Assets", "") + newFilePath;
        string scriptContent = File.ReadAllText(realPath);

        //这里实现自定义的一些规则  
        scriptContent = scriptContent.Replace("#SCRIPTFULLNAME#", Path.GetFileName(newFilePath));
        scriptContent = scriptContent.Replace("#COMPANY#", PlayerSettings.companyName);
        scriptContent = scriptContent.Replace("#AUTHOR#", "Passion");
        scriptContent = scriptContent.Replace("#VERSION#", "1.0");
        scriptContent = scriptContent.Replace("#UNITYVERSION#", Application.unityVersion);
        scriptContent = scriptContent.Replace("#DATE#", System.DateTime.Now.ToString("yyyy-MM-dd hh:mm:ss"));

        File.WriteAllText(realPath, scriptContent);
    }
}
```

然后呢每当在本工程下新建C#脚本的时候就会自动生成注释模板。




