[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/saliton/Capitalize/blob/master/Capitalize.ipynb)

# 英文をちゃんとキャピタライズしたい

ある英語のチャットボットを試した時、以下のように出力してくるものがありました。<br>
> that ' s cool . i like watching sports . do you have any hobbies besides tennis ?<br>

人間なら特に問題なく読めるのですが、これを機械翻訳に連携させた時に困ったことがありました。翻訳の品質が落ちてしまうものがあったのです。ちゃんとキャピタライズさせてから入力したほうがはるかに翻訳品質がよかった。

というわけで、キャピタライズする関数を書いてみました。



```Python
import re

def upperEnd(obj):
    '''引数の末尾を大文字にする'''
    return obj.group()[:-1] + obj.group()[-1].upper()

def capitalize(text):
    '''文をキャピタライズする'''
    text = re.sub(r'\s*([\.?!,])', r'\1', text)     # 句読点の前の空白を削除する
    text = re.sub(r"\s'\s", "'", text)            # 'の前後の空白を削除する
    text = re.sub(r'[\.?!:]\s+.', upperEnd, text) # 句点の後の最初の文字を大文字にする
    text = text[0].upper() + text[1:]           # 文の最初の文字を大文字にする
    return text

print(capitalize("that ' s cool . i like watching sports . do you have any hobbies besides tennis ?"))
```

    That's cool. I like watching sports. Do you have any hobbies besides tennis?


以上です。何かの参考になれば
