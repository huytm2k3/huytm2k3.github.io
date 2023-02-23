---
title: Blazor for Beginner
date: 2023-02-08 08:42:14
tags: [C#, Fullstack]
---

## Blazor là gì?

Blazor là UI Framework sử dụng .NET cho phép Developers phát triển, xây dựng giao diện người dùng thông qua HTML, C# và Razor Templates.

## Cài đặt Blazor

Blazor: https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor

## Tạo mới project Blazor

Xem danh sách Project Template của .NET

```bash
dotnet new // show all dotnet project template
```

Tạo Project Blazor

```bash
dotnet new blazorserver -o FirstBlazorApp
```

## Blazor notes

Với razor template, có thể using và import sử dụng như ReactJS:

```cs
@using BlazorServerAppDemo.Pages.ContactComponents
<ContactComponent01 contact=@contact DeleteCurrentContact="DeleteContact" ></ContactComponent01>
```

Callback, Index.razor chứa List Object contacts, vậy trong ContactComponent01 làm sao để gọi hàm xóa được các elements ở index: Sử dụng callback

Index.razor:

```cs
private void DeleteContact(Contact contact)
{
    contacts.Remove(contact);
}
```

ContactComponent01.razor:

```cs
<button @onclick="@(() => DeleteCurrentContact.InvokeAsync(contact))">Delete</button>
@code{

	[Parameter]
	public EventCallback<Contact> DeleteCurrentContact { get; set; }

}
```

Lấy ra ChildContent giống {Children} trong React:

```cs
@ChildContentA
@ChildContentB

@code{
    [Parameter]
    public RenderFragment ChildContentA { get; set; }
    public RenderFragment ChildContentB { get; set; }
}
```

Gửi đi ChildContent:
```cs
<App>
    <ChildContentA>
        <h1>Content A</h1>
    </ChildContentA>
    <ChildContentB>
        <h1>Content B</h1>
    </ChildContentB>
</App>
```
