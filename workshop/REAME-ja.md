# セットアップ概要

次のセクションでは、Minishiftのインストール方法と必要な依存関係について説明します。

これらは、パーソナルシステムでMinishiftをセットアップするための基本的な手順です。

1. [仮想化環境の構成](./#configure-the-virtualization-environment)
2. [Minishiftのダウンロードとインストール](./#download-and-install-minishift)
3. [OpenShiftサーバーの起動](./#start-the-openshift-server)

セットアップ手順は、仮想マシンを起動する権限を持つ通常のユーザーとして実行する必要があります。 手順では、ハイパーバイザーとコマンドシェルを構成してMinishiftを起動し、効果的に対話する方法と共に、そのアクセス許可を割り当てる方法について説明します。

# 仮想化環境を構成する

MinishiftはWindows、Linux、およびMacにインストールできますが、プラットフォームによっては、OpenShiftクラスターを仮想化環境内に作成するために、互換性のあるハイパーバイザーを構成する必要があります。 Minishiftをセットアップする前に、選択したハイパーバイザーがシステムにインストールされ、有効になっていることを確認してください。 ハイパーバイザーが稼働したら、Minishiftがそのハイパーバイザーと連携するために追加のセットアップが必要です。
ハイパーバイザーとオペレーティングシステムに該当するセクションを参照してください。

- For Linux, [set up the KVM driver](https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-kvm-driver)
- For macOS, ~~[set up the xhyve driver](https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-xhyve-driver)or~~ [set up the hyperkit driver](https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-hyperkit-driver)
- For Windows, [set up the Hyper-V driver](https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-hyperkit-driver)
- For VirtualBox (all platforms), [set up Minishift to use VirtualBox](https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html#setting-up-virtualbox-driver)

*メモ: Macにdocker-ceをマシンにインストールした場合、ハイパーキットドライバーは既にインストールされています*

# Minishiftをダウンロードしインストールする

[Minishiftをダウンロード](https://docs.okd.io/latest/minishift/getting-started/installing.html) するには、ソースからインストールするか、Macの場合はHomebrewを使用してインストールできます。 

# OpenShiftサーバーの開始

前の手順を正常に完了していれば、OpenShiftサーバーを起動する準備が整ってます。 サーバーを開始するには、次を実行する必要があります。

```
$ minishift start --vm-driver <driver>
```

`<driver>`を使用するドライバーに置き換えてください。 「ハイパーキット」または「仮想ボックス」。 正常に開始されると、以下に示すように、クラスターにログインするための資格情報とUIアドレスが提供されます。
```
OpenShift server started.

The server is accessible via web console at:
    https://192.168.64.11:8443/console

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin


-- Exporting of OpenShift images is occuring in background process with pid 5703.
```

*メモ: コンソールアドレスとpidはそれぞれ異なります。*

# さらにクラスターを構成する

クラスターをセットアップした後、クラスターに適用する特定の要件がある場合があります。 Minishiftツールを使用すると、シングルノードOpenShiftクラスターのライフサイクルを管理できるだけでなく、マシンがプロキシの背後にある場合は、環境変数、永続ストレージ、プロキシオプションを設定できます。 これらの構成の詳細については、次の [リンク](https://docs.okd.io/latest/minishift/using/basic-usage.html#runtime-options) を参照してください。
すべての設定が完了したら [Lab 1](./Lab1/README.md) に進むことができます。
