<details><summary>フラグ</summary>

flag{you_do_the_know_between_nces_differeand_a_typhoon_a_cyclone?}
</details>


<details><summary>説明</summary>
pythonコードは直接実行されず、pycというバイトコードに変換されてから仮想環境上で実行されます。
pycファイル形式は先頭16Byteにファイルヘッダーが配置され、その後にmarshalモジュールで変換された
コードオブジェクトが並びます。
pycファイルの16Byte以降を読み取り、marshalモジュールでコードモジュールに復元することで、
存在する関数情報を確認し、flag関数を実行可能です。
```py
with open("pythoon-typhoon.pyc", "rb") as f:
    import marshal
    f.read(16)
    code = marshal.load(f)
namespace = {}
exec(code, namespace)
print(namespace.keys())
print(namespace["flag"]())

# import dis
# dis.dis(code) # 関数情報から手作業復元も可能
```
</details>