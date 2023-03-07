---
title: .Net Maui App Upload file to Server
date: 2023-03-07 09:29:15
tags:
---
Sử dụng FilePicker, gắn sự kiện cho 1 Element
```cs
[RelayCommand]
		async void OnFilePicker()
        {
            IsRefreshing = true;
            IsRefreshing = false;
            var httpClient = new HttpClient();
            var result = await FilePicker.PickAsync(new PickOptions
			{
				PickerTitle = "Pick Image Please",
				FileTypes = FilePickerFileType.Images
			});
			if (result == null)
				return;

			using var content = new MultipartFormDataContent();
			var stream = await result.OpenReadAsync();
            var fileContent =
               new StreamContent(result.OpenReadAsync().Result);
            fileContent.Headers.ContentType =
                                    new MediaTypeHeaderValue(result.ContentType);
            content.Add(
                content: fileContent,
                name: "mfile",
                fileName: result.FileName
            );
            var response = await httpClient.PostAsync("http://localhost:5108/upload", content);

        }
```
