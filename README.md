# kubeconsole
Lowkey shell overlay for making life with kubectl a bit more bearable

Requirements:
- bash
- jq
- kubectl with a 'config' in '~/.kube'

## Getting started
### Make kubeconsole executable
```
chmod u+x kubeconsole
```
### Add a kube config
Add a file 'config' in '~/.kube' with your kubeconfig. 

Run 'kubeconsole -c' to get help on getting a kubeconfig, if you work at DBC. If not, ask
your local kubernetes guru for how to get a kubeconfig. 

```
./kubeconsole -c
```
### Making executing kubeconsole easier
Making life easier, by adding a symbolic link to kubeconsole in your local bin,
so you can run kubeconsole from any directory
```
:~/bin$ ln -s /path/to/your/checkout/kubeconsole/kubeconsole
```
You can now run kubeconsole from any where and do not need to provide the full path
/path/to/your/checkout/kubeconsole/kubeconsole

### Examples of commands
#### Activate kubeconsole (when you have symbolic link)
```
$ kubeconsole
```
#### Or activate kubeconsole with direct path to kubeconsole
```
$ /path/to/your/kubeconsole
```
This will now enter the kubeconsole shell (K8S) where you have access to a
number of commands and look something like this:
```
(K8S):~/user-<usr>$ 
```
#### Getting help
```
(K8S):~/user-<usr>$ h 
```
#### Set namespace (and see pods in namespace)
Command ns
```
(K8S):~/user-<usr>$ ns myservice-staging 
```
and your shell will now look like this
```
(K8S):~/myservice-staging$ 
```

#### Get pods 
Command pods (alias 'p')
```
(K8S):~/myservice-staging$ pods 
  1 = author-name-suggester-8448d67458-4nmsp               1/1       Running     1   27d
  2 = cowbrow-frontend-service-564f79d559-xsvwm            1/1       Running     0   40d
  3 = batch-exchange-loadtest-service-7856945fc5-fq9kp     1/1       Running     0   20h
```
or
```
(K8S):~/myservice-staging$ p 
  1 = author-name-suggester-8448d67458-4nmsp               1/1       Running     1   27d
  2 = cowbrow-frontend-service-564f79d559-xsvwm            1/1       Running     0   40d
  3 = batch-exchange-loadtest-service-7856945fc5-fq9kp     1/1       Running     0   20h
```

#### Filter results
Command filter
```
(K8S):~/myservice-staging$ filter frontend 
```
and your shell will now look like this
```
(K8S):~/myservice-staging/frontend$ 
```
and if you now get pods you will only see ones with "frontend" in their name
```
(K8S):~/myservice-staging/frontend$ p 
  1 = cowbrow-frontend-service-564f79d559-xsvwm            1/1       Running     0   40d
```
To remove filter just type filter
```
(K8S):~/myservice-staging/frontend$ filter
```
and you're back to 
```
(K8S):~/myservice-staging$
```
#### Show log
Command log - it default set to log from last hour. See help for how to change that
```
(K8S):~/myservice-staging$ p

  1 = author-name-suggester-8448d67458-4nmsp               1/1       Running     1          27d
  2 = cowbrow-frontend-service-564f79d559-xsvwm            1/1       Running     0          40d
  3 = batch-exchange-loadtest-service-7856945fc5-fq9kp     1/1       Running     0          20h
```
Show log from pod no. 1 - log 1

```
(K8S):~/myservice-staging$ log 1
kubectl logs author-name-suggester-8448d67458-4nmsp --since=1h -n metascrum-staging
[pid: 48|app: 0|req: 515822/802444] 10.233.24.1 () {34 vars in 401 bytes} [Tue Nov 12 10:04:06 2019] GET /api/status => generated 15 bytes in 15 msecs (HTTP/1.1 200) 1 headers in 51 bytes (15 switches on core 0)
[pid: 48|app: 0|req: 515823/802445] 10.233.24.1 () {34 vars in 401 bytes} [Tue Nov 12 10:04:09 2019] GET /api/status => generated 15 bytes in 15 msecs (HTTP/1.1 200) 1 headers in 51 bytes (16 switches on core 0)
```



## Trouble shooting
Did you get the error message
```
bash: /home/usr/.kubeconsole/complete: No such file or directory
```
Then you need to add a new kubeconfig to 'config' in '~/.kube'

## Getting more help 
No further documentation, but you may find the command "help" or 'kubeconsole -h' useful ;)
```
./kubeconsole -h
```
---

## If you want to contribute
Please keep this simple - this is not supposed to be a huge tool that
can fix the whole world, just make life a bit more easy.

Please dont push to master, use normal Git flow.

Please dont hang me for the huge amount of redundancy and too-simple
bash'ing, it's just a tool that has been banged together over a single
lab-day with too much coffee in the blood.

HWHA Sept. 2019


