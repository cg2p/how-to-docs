# intro to Operators
https://developers.redhat.com/blog/2020/08/21/hello-world-tutorial-with-kubernetes-operators/120100/?sc_cid=7013a000002h14YAAQ

- install operator sdk
`brew install operator-sdk`

```
operator-sdk version

operator-sdk init --project-name=reverse-app-operator --repo=github.com/cg2p/reverse-app-operator

operator-sdk create api --group cg2p --version v1beta1 --kind Reverse
> y to create resource and controller


```
