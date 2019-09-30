# Lab 1. Creating OpenShift projects

Learn how to login to an OpenShift cluster and create a new project in Minishift.

## 1. Login to the cluster

Login to the cluster with the output from the command after running `minishift start` as described in [setup overview](../README.md).

```
$ oc login -u system:admin
```

If you get an error about the `oc` command not being found, you can source it with the following command:

```
$ eval $(minishift oc-env)
```

As you will be able to see, there are several projects available to be able to switch between different workloads.

## 2. Create a project

You should have a default project setup already but we will create a new project for our new application. 

```
$ oc new-project nodejs-echo --display-name="nodejs" --description="Sample Node.js app"
```

Now you should have a new project with the label `nodejs` and your active project will now point to it. If you want to switch between projects, run:

```
$ oc project <display-name>
```

Congratulations, you have logged into your cluster and have created your first OpenShift project! To learn how to create your first application move on to the [next lab (Lab 2)](../Lab2/README.md).




＃Lab1. OpenShiftプロジェクトの作成

OpenShiftクラスターにログインし、Minishiftで新しいプロジェクトを作成する方法を学びます。

## 1.クラスターにログインします

[セットアップの概要]（../README-ja.md）で説明されているように、 `minishift start`を実行した後、コマンドの出力を使用してクラスターにログインします。

```
$ oc login -u system：admin
```

`oc`コマンドが見つからないというエラーが表示された場合、次のコマンドを使用してソースを取得できます。

```
$ eval $(minishift oc-env)
```

ご覧のとおり、さまざまなワークロードを切り替えることができるプロジェクトがいくつかあります。

## 2.プロジェクトを作成する

デフォルトのプロジェクト設定がすでにあるはずですが、新しいアプリケーション用に新しいプロジェクトを作成します。

```
$ oc new-project nodejs-echo --display-name="nodejs" --description="Sample Node.js app"
```

これで、ラベルが「nodejs」の新しいプロジェクトが作成され、アクティブなプロジェクトがそれを指すようになります。プロジェクトを切り替える場合は、次を実行します。

```
$ oc project <display-name>
```

おめでとうございます。クラスターにログインし、最初のOpenShiftプロジェクトを作成しました。最初のアプリケーションの作成方法を学習するには、[次のラボ（ラボ2）]（../Lab2/README-ja.md）に進みます。
