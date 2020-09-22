# 개요

WPF 실행 화면에서 테스트 할 파일의 위치를 지정하거나 테스트 한 결과가 저장된 Excel 파일이나 Json 파일을 찾아야 하는 경우가 생겼다. 따로 폴더를 열어서 파일을 찾는거보다 지정된 디렉토리 경로를 저장하는 게 있기 때문에 프로그램에서 폴더를 열어주는 것이 더 빠르다 생각하였다. 그래서 파일을 UI에서 바로 열 수 있는 방법을 찾아보았다.

파일과 폴더 각각 C#에서 제공해주는 메소드가 다르다.

## 1. OpenFileDialog

파일을 찾기 위해선 `OpenFileDialog` 메소드를 사용한다. `OpenFileDialog` 가 실행되면 윈도우에서 제공해주는 파일 찾기 폼이 나온다. 폼 내에서 파일을 찾아서 확인을 누르면 파일 경로를 획득할 수 있다.

처음에 파일을 찾기 시작할 초기 경로와 폼 오른쪽 아래에 있는 찾으려는 양식의 필터를 설정할 수 있다.

파일 경로를 선택 후 획득하면 `Process.Start()` 같은 파일을 여는 메소드에 파일 경로를 넣어 실행할 수 있다.

```csharp
public void SelectFilePath(string FileSrc, string FileType)
{
    FileInfo FileName;

    OpenFileDialog FileOpenDialog = new OpenFileDialog();
    {
				// 초기 경로 설정
        FileOpenDialog.InitialDirectory = FileSrc;
				// 파일 양식 설정
        FileOpenDialog.Filter = "All Files | *.*";
				
				// 파일 및 경로가 존제하는 지 확인
        FileOpenDialog.CheckFileExists = true;
        FileOpenDialog.CheckPathExists = true;

        if (FileOpenDialog.ShowDialog().GetValueOrDefault())
        {
            FileName = new FileInfo(FileOpenDialog.FileName);
						
						// 파일 종류에 따른 여는 방식을 Switch문으로 구현
            switch (FileType)
            {
                case "xlsx":
                    Excel.Application application = new Excel.Application();
                    application.Workbooks.Open(Filename: FileName.FullName);
                    application.Visible = true;
                    break;
                case "json":
                    Process.Start(FileName.FullName);
                    break;
            }
        }
    }
}
```

## 2. FolderBrowserDialog

위에 있는 `OpenFileDialog` 과 달리 `FolderBrowserDialog` 는 파일의 경로를 찾아주는 메소드이다.

`FolderBrowserDialog` 를 실행하면  `OpenFileDialog` 와 달리 작은 창이 뜨게 된다.

프로그래밍 할 때 `OpenFileDialog` 와 큰 차이 없이 작성 가능하다.

```csharp
public void ShowOpenFileDialog(string File)
{
		OpenFileDialog OFD = new OpenFileDialog();
		// 창 제목 지정
		OFD.Title = "Browse For Folder";
		// 필터 지정
		OFD.Filter = "All file | *.*";
		
		if(OFD.ShowDialog() == DialogResult.OK)
		{
				// 파일 경로 획득
				file = OFD.FileName;
		}
}
```

## 3. CommonOpenFileDialog

만약 `OpenFileDialog` 을 사용하면서 `FolderBrowserDialog` 을 사용하면 두 창의 생김새가 달라 통일성이 떨어진다. 동일한 창이 뜨게 하기 위해 `CommonOpenFileDialog` 메소드를 사용한다.

CommonOpenFileDialog` 를 사용하기 위해선 NuGet에서 `WindowsAPICodePack`을 다운받아야 한다. `WindowsAPICodePack-Core` 와 `WindowsAPICodePack-Shell`을 설치하자.

> [Github](https://github.com/aybe/Windows-API-Code-Pack-1.1)에서 `CommonOpenFileDialog` 이외에도 `WindowsAPICodePack` 에서 사용할 수 있는 라이브러리를 확인할 수 있다.

코드 작성은 앞에서 말했던 두 메소드와 방식이 비슷하다. 메소드를 선언하고 폴더를 클릭하면 폴더 이름을 가져올 수 있다.

```csharp
public string ChangeFolderPath()
{
		string FilePath = "";		
    CommonOpenFileDialog dialog = new CommonOpenFileDialog();
    {
        dialog.IsFolderPicker = true;

        if (dialog.ShowDialog() == CommonFileDialogResult.Ok)
        {
            FilePath = dialog.FileName;
        }
    }

		return FilePath;
}
```

# 여담

**"세 개의 메소드 다 쓰는 방식이 비슷하다."**

쉽게 사용할 수 있도록 제작한 폼이라 별 무리없이 사용이 가능했다. 사용방식이 너무 비슷해서 글 쓸 내용도 크게 없었다. 그만큼 편리하게 사용이 가능하므로 적제적소에 잘 사용하는 것이 중요하다 생각한다. 평소에 파일을 찾을 때 저런 파일을 찾는 창이 열리는 것이 귀찮다고 생각해서 드레그 엔 드롭도 생각해봤지만 개발 일정을 고려해서 따로 더 넣지 않았다. 대신 메소드 내 설정을 잘 활용해서 사용자가 원하는 위치로 최소한의 클릭을 사용해 갈 수 있도록 설정할 수 있다. 효율적으로 사용하는 것이 중요하다.