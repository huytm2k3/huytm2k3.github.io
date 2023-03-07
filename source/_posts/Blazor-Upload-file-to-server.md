---
title: .Net Blazor Upload file to server
date: 2023-03-07 07:14:59
tags:
---

1. Phía Client

```c#
@page "/file-upload"
@using System.Net.Http.Headers;
@using lifeloggers_web_7._0.Models;
@inject IJSRuntime jsRuntime;

<PageTitle>Upload Files</PageTitle>


<InputFile OnChange="OnInputFileChange" multiple />

@code {
    private FileModel mfile = new FileModel();
    private async void OnInputFileChange(InputFileChangeEventArgs e)
    {
        var httpClient = new HttpClient();
        var selectedFiles = e.GetMultipleFiles();
        var message = $"{selectedFiles.Count} file(s) selected";
        foreach (var file in e.GetMultipleFiles())
        {
            using var content = new MultipartFormDataContent();
            var fileContent =
                new StreamContent(file.OpenReadStream());
            fileContent.Headers.ContentType =
                                    new MediaTypeHeaderValue(file.ContentType);
            content.Add(
                content: fileContent,
                name: "mfile",
                fileName: file.Name
            );
            var response = await httpClient.PostAsync("http://localhost:5108/upload", content);
        }
    }
}
```

2. Phía server (ASP.Net core Web API)

Service:

```cs
public async Task<string> Upload([FromForm] File mFile)
		{
			var lastFile = new FileMongo {};
			if(mFile.mfile.Length > 0)
			{
				var path = Path.Combine(Directory.GetCurrentDirectory(), "wwwroot", "images", mFile.mfile.FileName);
				using (var stream = System.IO.File.Create(path))
				{
					await mFile.mfile.CopyToAsync(stream);
				}
				lastFile.Path = "/images/" + mFile.mfile.FileName;
				await _filesCollection.InsertOneAsync(lastFile);
			}
			return "ok";
		}
```

Controller

```cs
[HttpPost("upload")]
		public async Task<string> Upload([FromForm] File mFile)
		{
			await _fileService.Upload(mFile);
			return "Successfully!";
		}
```
