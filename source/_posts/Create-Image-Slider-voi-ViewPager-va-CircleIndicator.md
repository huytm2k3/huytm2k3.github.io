---
title: Create Image Slider với ViewPager và CircleIndicator
date: 2022-06-08 10:11:42
tags: [android, javaOOP, image-slider]
categories: [Front-end]
---

## Mở đầu

Image Slider giúp chúng ta trình chiếu hình ảnh, CircleIndicator là những dấu chấm tròn hiển thị số lượng và thứ tự ảnh, 2 thứ này dùng rất nhiều trong những dự án android thực tế.

Mọi thắc mắc xin liên hệ tới:
- Facebook: https://www.facebook.com/profile.php?id=100072417355186 (Tạ Minh Huy)
- Zalo: 0522566897
- Email: Huyat180522@gmail.com

## Kiến thức yêu cầu

Java OOP

## Ví dụ thực tế

![](/images/ImageSliderPost/a1.png) 

## Thực hiện

### 1. Implementation thư viện cần thiết

```java
dependencies {
    //noinspection GradleCompatible
    implementation 'me.relex:circleindicator:2.1.6'
    ...
}
```
### 2. Tạo model chứa thuộc tính cần slide (Ở đây chúng ta chỉ cần 1 ImageView)

```java
package mhuy.com.hnshop;

public class Photo {
    private int resourceId;

    public Photo(int resourceId) {
        this.resourceId = resourceId;
    }

    public int getResourceId() {
        return resourceId;
    }

    public void setResourceId(int resourceId) {
        this.resourceId = resourceId;
    }
}

```
### 3. Tạo 1 layout chứa duy nhất 1 ImageView (item_photo.xml)

``` xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ImageView
        android:id="@+id/img_photo"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:scaleType="centerCrop"
        />

</LinearLayout>
```


### 4. Tạo Adapter extends PagerAdapter, implement và sửa một số method như sau:
```java
package mhuy.com.hnshop;

import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;

import androidx.annotation.NonNull;
import androidx.viewpager.widget.PagerAdapter;

import java.util.List;

public class PhotoViewPagerAdapter extends PagerAdapter {

    private List<Photo> mListPhoto;

    public PhotoViewPagerAdapter(List<Photo> mListPhoto) {
        this.mListPhoto = mListPhoto;
    }



    @NonNull
    @Override
    public Object instantiateItem(@NonNull ViewGroup container, int position) {
        View view = LayoutInflater.from(container.getContext()).inflate(R.layout.item_photo, container, false);
        ImageView imgPhoto = (ImageView) view.findViewById(R.id.img_photo);

        Photo photo = mListPhoto.get(position);
        imgPhoto.setImageResource(photo.getResourceId());

        // add View

        container.addView(view);

        return view;
    }

    @Override
    public int getCount() {
        if(mListPhoto != null){
            return mListPhoto.size();
        }
        return 0;
    }

    @Override
    public boolean isViewFromObject(@NonNull View view, @NonNull Object object) {
        return view == object;
    }

    @Override
    public void destroyItem(@NonNull ViewGroup container, int position, @NonNull Object object) {
        container.removeView((View) object);
    }
}

```

### 5. Thêm 1 số hình ảnh cần slide vào thư mục res/drawable
![](/images/ImageSliderPost/a2.png)


<!--more-->

### 6. Ở class MainActivity, ánh xạ ViewPager, dùng Adapter và List để khởi tạo ViewPager
```java
package mhuy.com.hnshop;

import androidx.appcompat.app.AppCompatActivity;
import androidx.viewpager.widget.ViewPager;

import android.os.Bundle;

import java.util.ArrayList;
import java.util.List;

import me.relex.circleindicator.CircleIndicator;

public class MainActivity extends AppCompatActivity {

    private ViewPager mViewPager;
    private CircleIndicator mCircleIndicator;
    private List<Photo> mListPhoto;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mViewPager = (ViewPager) findViewById(R.id.view_pager);
        mCircleIndicator = (CircleIndicator) findViewById(R.id.circle_indicator);

        mListPhoto = getListPhoto();

        PhotoViewPagerAdapter adapter = new PhotoViewPagerAdapter(mListPhoto);
        mViewPager.setAdapter(adapter);

        mCircleIndicator.setViewPager(mViewPager);
    }

    private List<Photo> getListPhoto(){
        List<Photo> list = new ArrayList<>();

        list.add(new Photo(R.drawable.img_1));
        list.add(new Photo(R.drawable.img_2));
        list.add(new Photo(R.drawable.img_3));
        list.add(new Photo(R.drawable.img_4));

        return list;
    }
}
```