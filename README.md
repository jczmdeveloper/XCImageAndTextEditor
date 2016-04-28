# XCImageAndTextEditor
A Mix Picture And Text Editor-使用SpannableString And ImageSpan 实现的图文混排编辑器
(下载Demo编译运行前：请在自己手机对应的包名的files/DCIM 目录下 放入对应的 5张 jpg图片，否则插入图片会报错)

效果图如下：


![image](https://github.com/jczmdeveloper/XCImageAndTextEditor/blob/master/screenshots/01.gif)  


![image](https://github.com/jczmdeveloper/XCImageAndTextEditor/blob/master/screenshots/02.jpg)  


使用方法示例如下：

package com.czm.demo;

import android.os.Bundle;
import android.os.Environment;
import android.support.v7.app.AppCompatActivity;
import android.text.Editable;
import android.text.TextWatcher;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import com.czm.xcimageandtexteditor.R;
import com.czm.xcimageandtexteditor.XCImageAndTextEditor;

public class MainActivity extends AppCompatActivity {
    private XCImageAndTextEditor mEditText;
    private Button mButton;
    private TextView mTextView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mEditText = (XCImageAndTextEditor) findViewById(R.id.edit_text);
        mButton = (Button) findViewById(R.id.button_add_picture);
        mTextView = (TextView)findViewById(R.id.textView);


        mButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                mEditText.insertBitmap(getDrawablePath());
                mTextView.setText(mEditText.getText().toString());
            }
        });

        mEditText.addTextChangedListener(new TextWatcher() {
            @Override
            public void beforeTextChanged(CharSequence s, int start, int count, int after) {

            }

            @Override
            public void onTextChanged(CharSequence s, int start, int before, int count) {
                Log.v("czm",mEditText.getContentList().toString());
            }

            @Override
            public void afterTextChanged(Editable s) {

            }
        });
    }

    int num = 0;
    public String getDrawablePath(){
        if(num >= 5){
            num = 1;
        }else{
            num ++;
        }
        return getExternalFilesDir(Environment.DIRECTORY_DCIM).getPath()+"/a"+num+".jpg";
    }
}

