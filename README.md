# home-kubernetes-metrics

## fluent-bit

baselimeのAPI_KEYをコピーしたら次のコマンドを実行する

```bash
$ kubectl -n vault exec -it vault-0 -- sh 
$ vault kv put kv/fluent-bit/baselime BASELIME_API_KEY=<API_KEY>
$ vault policy write read-baselime -  << EOF
path "kv/data/fluent-bit/baselime" {
    capabilities = ["read"]
}
EOF
$ vault write auth/kubernetes/role/read-baselime \
bound_service_account_names=default \
bound_service_account_namespaces=fluentbit-system \
policies=read-baselime
```