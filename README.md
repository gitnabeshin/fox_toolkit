# fox_toolkit
learning Fox Toolkit

# About
FOX is a C++ based Toolkit for developing Graphical User Interfaces
* http://www.fox-toolkit.org

# DevEnv
* Windows 10
* VisualStudio 2017
    * Windows 8.1 SDK
    * UWP用 Windows 10 SDK (10.0.16299.0): C++
    * デスクトップ C++用 Windows 10 SDK (10.0.16299.0) [x86, x64]

# Setup & Build

## 1. Download
* Fox for win(Windows XP/WIN7/WIN10)    via ftp or http
    * http://fox-toolkit.org/ftp/fox-1.6.57.zip
    * ftp://ftp.fox-toolkit.org/pub/fox-1.6.57.zip
* Unzip
    * `C:/Users/nabeshin/source/fox-1.6.57`

```
$ pwd
C:/Users/nabeshin/source/fox-1.6.57/windows/vcpp
$ ls
adie            datatarget  fox         hello       mditest         scribble    table
bitmapviewer    dctest      foxdll      hello2      memmap          shutter     wizard
button          dialog      gltest      iconlist    minheritance    shutterbug  win32.dsw
calculator      dirlist     glviewer    image       pathfinder      splitter
chart           expression  groupbox    imageviewer ratio           switcher
chartdll        foursplit   header      layout      reswrap         tabbook
```

* fox
   * FOX.lib
* Others
   * Sample Applications(exe)


## 2. Open & convert project

* Open win32.dsw with VisualStudio 2017
    * `C:¥Users¥nabeshin¥source¥fox-1.6.57¥windows¥vcpp¥win32.dsw`
    * Convert project into VS2017.


## 3. Build Fox.lib

### 3.1 "fox" projectのプロパティを表示し、以下を設定。

全ての構成で以下を追加。

* 全般
    * 構成の種類
        * `スタティックライブラリ(.lib)`
    * Windows SDK Version
        * `8.1`
* VC++ ディレクトリ
    * インクルードディレクトリ
        * `C:/Program Files(x86)/Windows Kits/10/Include/10.0.17763.0/ucrt`
* C/C++
    * プリプロセッサ
        * プリプロセッサの定義
            * `WIN32;HAVE_VSSCANF;HAVE_STRTOLL;HAVE_STRTOULL;`
    * 全てのオプション
        * 関数レベルでリンクする
            * `はい(/Gy)`

### 3.2 Build

* 出力先
    * `C:¥Users¥nabeshin¥source¥fox-1.6.57¥lib¥FOX-1.6.lib`
    * `C:¥Users¥nabeshin¥source¥fox-1.6.57¥lib¥FOXD-1.6.lib`

## 4. 各種サンプルプロジェクトの実行

以下の fox 以外がサンプル。

```
adie            datatarget  hello       mditest         scribble    table
bitmapviewer    dctest      hello2      memmap          shutter     wizard
button          dialog      gltest      iconlist    minheritance    shutterbug
calculator      dirlist     glviewer    image       pathfinder      splitter
chart           expression  groupbox    imageviewer ratio           switcher
chartdll        foursplit   header      layout      reswrap         tabbook
```

### 4.1 projectのプロパティを追加。

全ての構成で以下を追加。

* 全般
    * 構成の種類
        * `アプリケーション(exe)`
    * Windows SDK Version
        * `8.1`
    * 出力ディレクトリ
        * `$(SolutionDir)$(Configuration)/`
    * 中間ディレクトリ
        * `$(Configuration)/`
* VC++ ディレクトリ
    * インクルードディレクトリ
        * `C:/Program Files(x86)/Windows Kits/10/Include/10.0.17763.0/ucrt`
    * ライブラリディレクトリ
        * `C:/Program Files(x86)/Windows Kits/10/Lib/10.0.17763.0/ucrt`
* C/C++
    * 全てのオプション
        * 関数レベルでリンクする
            * `はい(/Gy)`
* リンカ
    * 出力ファイル
        * `$(OutDir)$(TargetName)$(TargetExt)`

### 4.2 Build

* 出力先
    * `C:¥Users¥nabeshin¥source¥fox-1.6.57¥windows¥vcpp¥Debug`

### 4.3 Execute

exe を指定して実行。

```
button.exe
calculator.exe
hello.exe
hello2.exe
layout.exe
splitter.exe
```

## 5. コンソールアプリからの呼び出し

### 5.1 プロジェクトの設定

* 新規プロジェクト作成で `コンソールアプリ` を作成。
* プロジェクトの設定で、以下を追加。
    * VC++ ディレクトリ
        * インクルードディレクトリ
            * `C:¥Users¥nabeshin¥source¥fox-1.6.57¥include`
        * ライブラリディレクトリ
            * `C:¥Users¥nabeshin¥source¥fox-1.6.57¥lib`
    * リンカ
        * 入力
            * 追加の依存ファイル `FOX-1.6.lib` (debugの場合は `FOXD-1.6.lib` )

### 5.2 サンプルコード

```
#include "fx.h"

int main(int argc,char **argv)
{
	FXApp application("AppName","VendorName"); 
	application.init(argc, argv);
	FXMainWindow* main = new FXMainWindow(&application,
                                          "FoxSample",
	                                      NULL,
                                          NULL,
                                          DECOR_ALL,
	                                      0,
                                          0,
	                                      600,
                                          400);
	application.create();
	main->show(PLACEMENT_SCREEN);
	return application.run();
}
```
