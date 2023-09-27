# podman-test

## 参考資料

- 「標準テキスト CentOS8 構築・運用・管理パーフェクトガイド」にて学習

## NextCloud のコンテナイメージを持ち運ぶ

- コンテナイメージをダウンロードする

    ```sh
    podman pull docker.io/library/nextcloud:latest
    ```

- コンテナイメージをファイル化

    ```sh
    podman save -o nextcloud-container-image.tar docker.io/library/nextcloud:latest
    ```

- PCにダウンロードしたコンテナを削除

    ```sh
    $ podman images
    REPOSITORY                   TAG         IMAGE ID      CREATED      SIZE
    docker.io/library/nextcloud  latest      aca08bdaba01  5 days ago   1.23 GB
    docker.io/library/httpd      latest      359570977af2  6 days ago   173 MB
    docker.io/library/ubuntu     latest      c6b84b685f35  5 weeks ago  80.4 MB
    quay.io/centos/centos        latest      300e315adb2f  2 years ago  217 MB
    [kazuhiro@localhost ~]
    $ podman rmi podman save -o nextcloud-container-image.tar docker.io/library/nextcloud:latest^C
    [kazuhiro@localhost ~]
    $ podman rmi aca08bdaba01
    Untagged: docker.io/library/nextcloud:latest
    Deleted: aca08bdaba013bcb8bf0befbd1911df8d8561e6c2378a11fdb234ee9785389e2
    [kazuhiro@localhost ~]
    $ podman images
    REPOSITORY                TAG         IMAGE ID      CREATED      SIZE
    docker.io/library/httpd   latest      359570977af2  6 days ago   173 MB
    docker.io/library/ubuntu  latest      c6b84b685f35  5 weeks ago  80.4 MB
    quay.io/centos/centos     latest      300e315adb2f  2 years ago  217 MB    
    ```

- ファイル化しコンテナイメージをロード

    ```sh
    podman load -i nextcloud-container-image.tar 
    ```

    ```sh
    odman images
    REPOSITORY                   TAG         IMAGE ID      CREATED      SIZE
    docker.io/library/nextcloud  latest      aca08bdaba01  5 days ago   1.23 GB
    docker.io/library/httpd      latest      359570977af2  6 days ago   173 MB
    docker.io/library/ubuntu     latest      c6b84b685f35  5 weeks ago  80.4 MB
    quay.io/centos/centos        latest      300e315adb2f  2 years ago  217 MB
    ```

- nextcloud のコンテナを実行

    ```sh
    podman run -d -p 8080:80 nextcloud
    ```

    ```sh
    $ curl http://10.1.1.201:8080
    ```

<del>
## 11-3 Podman

### 11-3-3 コンテナの生成/管理で利用されるLinuxカーネル機能
</del>

- ★一旦ここで終了