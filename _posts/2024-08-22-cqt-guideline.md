# Put C++ Constant-Q Transform Code into Visual Studio Solution
## 0x00 Build cqt-analyzer
Follow this guidance [document](https://github.com/jmerkt/cqt-analyzer/blob/main/README.md).

## 0x01 Generate artifacts
* Open cqt-analyzer solution in Visual Studio
  * My version of Visual Studio is v2022
  * My cqt-analyzer solution is in directory `D:\src\cqt-analyzer\CqtAnalyzer\build`, but urs maybe differ.
![image](https://github.com/user-attachments/assets/25d277e9-1ca8-4e8d-b01d-73297e34c762)
* Build
![image](https://github.com/user-attachments/assets/0283d2c7-c305-4b38-9e6e-57f3f4ae9a6e)
* Get the artifacts
  * Use the `Release` mode and `x64` platform, so the artifacts directory is `D:\src\cqt-analyzer\CqtAnalyzer\build\CqtAnalyzer_artefacts\Release\VST3\CqtAnalyzer.vst3\Contents\x86_64-win`, but urs maybe differ.
![image](https://github.com/user-attachments/assets/5061504e-5246-4ede-b41c-36d652f21ca8)
![image](https://github.com/user-attachments/assets/8d6dff8b-b8b5-425c-b944-36a6ed04df89)

## 0x02 Utilize the CqtAnalyzer.vst3 plugin for ur purpose
