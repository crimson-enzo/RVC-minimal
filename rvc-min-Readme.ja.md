[**English**](rvc-min-Readme.md) | [**日本語**](rvc-min-Readme.ja.md)

# プロジェクトセットアップ指示

このREADMEは、Python環境のセットアップとプロジェクトに必要なパッケージの準備についての詳細な指示を提供します。

**注意:** ビルドを行うメイン環境は、CPPリリースバージョンのライブラリとの互換性を保証するためにPython 3.9を使用する必要があります。

0. **GitHubからファイルをコピー：**

    最初に、指定されたGitHubページからすべてのファイルをCPPリリースディレクトリにコピーします。

## Python仮想環境のセットアップ

1. **CPPリリースディレクトリへのナビゲート：**

    CPPリリースディレクトリに移動して始めます：

    ```cmd
    cd <CPP_RELEASE_DIR>
    ```

2. **仮想環境の作成とアクティベーション：**

    現在のディレクトリに新しい仮想環境を作成します：

    ```cmd
    python -m venv .venv
    ```

    このコマンドは `.venv` という名前の新しいディレクトリを作成します。

    次に、仮想環境をアクティブにします：

    ```cmd
    .\.venv\Scripts\activate
    ```

    ターミナルのプロンプトが変わり、仮想環境の名前が表示され、それがアクティブであることを示します。

## PyTorchのインストール

3. **PyTorchのインストール：**

    PyTorchとともにtorchvisionとtorchaudioをインストールします：

    ```cmd
    pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
    ```

## 追加依存関係のインストール

4. **その他の必要なパッケージのインストール：**

    提供された `requirements.txt` ファイルを使用して、他の必要なパッケージをインストールします：

    ```cmd
    pip install -r rvc-min-requirements.txt
    ```

## CPPリリースディレクトリの更新

5. **`site-packages`の準備と更新：**

    既存の `site-packages` ディレクトリをリネームします：

    ```cmd
    ren "lib\site-packages" "site-packages_old"
    ```

    `.venv\Lib\site-packages` の内容をコピーします：

    ```cmd
    xcopy /E /I ".venv\Lib\site-packages" "lib\site-packages"
    ```

## オプショナルステップ

6. **`tkinter`の手動インストール：**

    Python 3.9が`tkinter`なしでインストールされている場合にエラーが発生したら、Pythonディストリビューションから`tkinter`フォルダを`lib\site-packages`ディレクトリに手動でコピーできます：

    ```cmd
    xcopy /E /I "tkinter" "lib\site-packages\tkinter"
    ```
   
    このステップは、Pythonインストールに`tkinter`が含まれていないことが確かな場合にのみ実行してください。
    
   `tkinter`ディレクトリを正常にコピーした後、現在のディレクトリから元の`tkinter`ディレクトリを削除できます：

    ```cmd
    rmdir /S /Q "tkinter"
    ```
   
    このステップは、現在のディレクトリに不要な`tkinter`フォルダをクリーンアップします。

## オプションのクリーンアップと最終化

7. **特定のディレクトリを 'to_remove' に移動：**

    ディレクトリが存在するかどうかを確認し、存在する場合はそれらを 'to_remove' ディレクトリに移動します：

    ```cmd
    md assets\to_remove
    move "assets\pretrained" "assets\to_remove"
    move "assets\pretrained_v2" "assets\to_remove"
    move "assets\uvr5_weights" "assets\to_remove"
    ```

    'hubert', 'rmvpe', および 'weights' を除くすべての不要なアセットファイルを削除します。

8. **古い `site-packages` ディレクトリの削除：**

    テストの後、`site-packages_old` ディレクトリを削除します：

    ```cmd
    rmdir /S /Q "lib\site-packages_old"
    ```

9. **最終的なクリーンアップ：**

    最後に、作成した仮想環境ディレクトリを削除します：

    ```cmd
    rmdir /S /Q ".venv"
    ```