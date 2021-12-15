# KARMADA-DASHBOARD
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/kubernetes/dashboard/blob/master/LICENSE)

Karmada Dashboard is a general purpose, web-based UI for Karmada which is a multi-cluster management project.
![image](docs/images/dashboard.png)

## QuickStart


### Prerequisites

#### Karmada
A karamada cluster which can be installed by this [tutorial](https://github.com/karmada-io/karmada/blob/master/README.md#install-karmada-control-plane)

#### Node
The current version of Karmada-dashboard requires node with version >= 8,recommended version is 8.17.0

---
### Install Karmada-dashboard

#### 1.Switch context to karmada-host
```bash
export KUBECONFIG="$HOME/.kube/karmada.config"
kubectl config use-context karmada-host
```
#### 2.Deploy karmada-dashboard
```bash

kubectl apply -f https://raw.githubusercontent.com/JCCE-nudt/karmada-dashboard/main/deploy/karmada-dashboard.yaml
```
when finish karmada-dashboard is able to access by http://karmada-host:30486 ,you still need to create an authentication token to access the dashboard.

#### 3.Create Service Account

To access dashboard，Service Account need to be created by executing commands below：

```bash
kubectl config use-context karmada-apiserver
kubectl apply -f  https://raw.githubusercontent.com/JCCE-nudt/karmada-dashboard/main/deploy/karmada-dashboard-role.yaml
```

#### 4.Get Bearer Token

To login dashboard, Bearer Token is required which can be generated by following commands:

```bash
kubectl -n karmada-system get secret $(kubectl -n karmada-system get sa/karmada-dashboard -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"
```

it should print results like this:
```bash
eyJhbGciOiJSUzI1NiIsImtpZCI6InZLdkRNclVZSFB6SUVXczBIRm8zMDBxOHFOanQxbWU4WUk1VVVpUzZwMG8ifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrYXJtYWRhLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJrYXJtYWRhLWRhc2hib2FyZC10b2tlbi14NnhzcCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJrYXJtYWRhLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImE5Y2RkZDc3LTkyOWYtNGM0MS1iZDY4LWIzYWVhY2E0NGJiYiIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDprYXJtYWRhLXN5c3RlbTprYXJtYWRhLWRhc2hib2FyZCJ9.F0BqSxl0GVGvJZ_WNwcEFtChE7joMdIPGhv8--eN22AFTX34IzJ_2akjZcWQ63mbgr1mVY4WjYdl7KRS6w4fEQpqWkWx2Dfp3pylIcMslYRrUPirHE2YN13JDxvjtYyhBVPlbYHSj7y0rvxtfTr7iFaVRMFFiUbC3kVKNhuZtgk_tBHg4UDCQQKFALGc8xndU5nz-BF1gHgzEfLcf9Zyvxj1xLy9mEkLotZjIcnZhwiHKFYtjvCnGXxGyrTvQ5rgilAxBKv0TcmjQep_TG_Q5M9r0u8wmxhDnYd2a7wsJ3P3OnDw7smk6ikY8UzMxVoEPG7XoRcmNqhhAEutvcJoyw
```

### Login Dashboard
Now open karmada-dashboard with url [http://karmada-host:30486 ](https://note.youdao.com/)(replace karmada-host to your own karmada host ip)
copy the token you just generated and paste it into the Enter token field on the login page.
![image](docs/images/login.png)

---
## License

Karmada is under the Apache 2.0 license. See the [LICENSE](LICENSE) file for details.
