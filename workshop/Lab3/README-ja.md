# Lab 3: OpenShiftアプリケーションの管理

[前のLab（Lab2）](../Lab2/README-ja.md) の指示に従ってOpenShiftアプリケーションを作成した後、次にそれが稼働中であることを確認し、アクセスする方法を確認していきましょう。

## 1. ビルドの監視

`oc new-app` を実行すると `docker build` のようにビルドが実行されます。 しかし `docker build` とは異なり、ビルドはバックグラウンドで行われ、実行内容は出力されません。

この出力を確認するには、次を実行します:

```console
$ oc status
```

試しに実行したいテンプレートをビルドします

```
$ oc new-app https://github.com/sclorg/nodejs-ex
```

ステータスを確認します:

```console
$ oc status
In project nodejs (nodejs-echo) on server https://192.168.64.11:8443

svc/nodejs-ex - 172.30.6.48:8080
  dc/nodejs-ex deploys istag/nodejs-ex:latest <-
    bc/nodejs-ex source builds https://github.com/sclorg/nodejs-ex on openshift/nodejs:10
      build #1 running for 36 hours
    deployment #1 waiting on image or update


2 infos identified, use 'oc status --suggest' to see details.
```

出力を見ると `172.30.6.48：8080` にあるNodeアプリにアクセスするためのサービスエンドポイントがあることがわかります。 また、アプリケーションの作成に使用されるビルドタイプである `openshift/nodejs:10` も確認できます。 そして最後の行で、アプリケーションがイメージのデプロイを待機しているため、実際に使用する準備ができていないことがわかります。 上記の行では、ビルド番号を使用して、ビルドで何が起こっているかをより包括的に把握できます。

アプリケーションのビルドの進行状況を確認したい場合、次のようにします:
```
$ oc logs build/<app-name>-<build-no>
```

この例では、アプリケーション名 `nodejs-ex` とビルド番号 `1` を使用します:
```
$ oc logs build/nodejs-ex-1
```

## 2. デプロイの監視

Kubernetesでは、実行中のすべてのアプリケーションのステータスを確認できます。 OpenShiftでは `oc` コマンドを使用する同じ機能があります:

```console
$ oc get pod
NAME                READY     STATUS      RESTARTS   AGE
nodejs-ex-1-build   0/1       Completed   0          13m
nodejs-ex-1-hx6v9   1/1       Running     0          12m
```

pod (`nodejs-ex-1-build`) がビルドを実行することのみを目的として作成され、正常に完了した後にクリーンアップされたことがわかります。 その後、Nodeアプリケーションを含む実行中のpod (`nodejs-ex-1-hx6v9`) が残ります。
関連付けられたポッドではなく、実際のアプリケーションである _deployments_ を実際に見たい場合、以下のように実行できます:

```console
$ oc get dc
NAME        REVISION   DESIRED   CURRENT   TRIGGERED BY
nodejs-ex   1          1         1         config,image(nodejs-ex:latest)
```

Kubernetesのもう1つの便利なコマンドは、アプリケーションに関連付けられているサービスがある場合に、それをチェックできる機能です。 Kubernetesで `kubectl get svc` を実行することでこれを行いますが、OpenShiftでも同様のことができます:

```console
$ oc get svc
NAME        TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)    AGE
nodejs-ex   ClusterIP   172.30.6.48   <none>        8080/TCP   14m
```

Kubernetesと同様に、各アプリケーションにはサービスにアクセスできる内部IPを与えることができますが、特に明記しない限り、これはクラスター内でのみ使用可能です。

おめでとうございます！ クラスター内でアプリケーションのビルドとデプロイを監視する方法を学びました！ OpenShiftクラスターの外部でアプリケーションを公開する方法を確認するために、[最終Lab（Lab4）](../Lab4/README-ja.md) に進みましょう。
