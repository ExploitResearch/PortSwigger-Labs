# Insecure direct object references

### Target Goal - 

find the password for the user `carlos`, and log into the account.

### Analysis/Exploitation -

- Select the **Live chat** tab.
- Send a message and then select **View transcript**.
**It’s sending a GET request to **`/download-transcript/2.txt`**! and we can see our own session’s transcript in response.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/43fe081c-ae5c-4bd3-938c-4c1e20dbf72b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663GKBI6P2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204647Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFpWlTxl7ILAo0Ogx%2FN%2FvSu%2BTIzdnEj0qn3C9izv7ZFRAiALCiZfVqKS2ceLRVrS9EzH1Rsqc%2F%2FFCe8Yz6pMqYqUayqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5eTY2IbdJ3mg5VBjKtwDk2kBKZK9laqoNgn94wojvqCI%2FqN2q1lqXPaqhOxS0pu%2FTXFt2KuQokGG1p5tARRoNroyjkKDfu4X%2BGc6Q1Wb1vkOS%2BM2OhFIt%2FYJgj%2BmB3vxrXYqpM8ElQ6eY2tpyVNQdShAW0Cd3LUI5ioqoP3ORuBn52jnuzWXobECVwA3qgQlBF6b2mK20pAwOaXv3kWJMb1KULBm3XeWoA0T4zB9Ds%2B%2BzZ6wAGso%2FWo%2FwZEk%2F67Z9Cg%2Faalo1tv3vFqoLWQYS0v8X1oklwHpkcKs8vOoAii5EalHBVD%2F94v%2BEf4cZiJmPxnrMl8hj4Q0t99qKGJVX5MNmwncHUTSpVXyOgAfDBqLpnKuJIJZi68rOgJ%2FdDNoEXYBVrSVZ1qOt4lZKHU9MAndXUwVCClkYr%2FSgJaAOrEZd1LbcZnrsqH4oJTV4wpkvqNEYqmORs3dXjUpZUUWWMqlol%2B7uZNzWsNEqlc3TZ0jMEbhsHmkr32cUY1KySdbo28O6Ys1cmXxKWpKQWgm%2FB%2Fux3slX7leKb975hSCNkgCrIcepUtrFPbGeZvkC%2FjoB349umSV1ZLSAHB%2FZerrUiWPHo33TAcO0vSUuIh8FpZYZAEcWdjMf5%2FOnR211IbugIwdY6ZHwUFSe7Iwisai1AY6pgHqYBUb%2FmNSNbi1ptTMMkbe0G%2FT1nRxFiRYHxdL6VUkrYFDUJPOdKPR6Gf7%2FCAt6IwM3ppN%2BePw%2FJeguJyw7XzmAXZF8pOqNRClS1JmPRMLfDYS94ppawuu%2BpazSo1Bq%2BXXbC%2BHtq7fJRZ37cRsuOCFiru02eYcUOrC3IfZ4bJ3NwoAdVvVveR3h2L9EZZbsuuIQiBUOVuufdVgiBG%2BwcWt1V4n46MD&X-Amz-Signature=069d5e6ee842581c91e79bb02a4cad1b03ab2211e017dbf215a4afe5387fa3d0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**What if I change the **`2.txt`** to **`1.txt`** Or **`3.txt`**, and so on?**

Change the filename to `1.txt` and review the text. Notice a password within the chat transcript.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c2f0a595-8a0c-45e3-ab3e-1abdbd8020c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663GKBI6P2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204647Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFpWlTxl7ILAo0Ogx%2FN%2FvSu%2BTIzdnEj0qn3C9izv7ZFRAiALCiZfVqKS2ceLRVrS9EzH1Rsqc%2F%2FFCe8Yz6pMqYqUayqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5eTY2IbdJ3mg5VBjKtwDk2kBKZK9laqoNgn94wojvqCI%2FqN2q1lqXPaqhOxS0pu%2FTXFt2KuQokGG1p5tARRoNroyjkKDfu4X%2BGc6Q1Wb1vkOS%2BM2OhFIt%2FYJgj%2BmB3vxrXYqpM8ElQ6eY2tpyVNQdShAW0Cd3LUI5ioqoP3ORuBn52jnuzWXobECVwA3qgQlBF6b2mK20pAwOaXv3kWJMb1KULBm3XeWoA0T4zB9Ds%2B%2BzZ6wAGso%2FWo%2FwZEk%2F67Z9Cg%2Faalo1tv3vFqoLWQYS0v8X1oklwHpkcKs8vOoAii5EalHBVD%2F94v%2BEf4cZiJmPxnrMl8hj4Q0t99qKGJVX5MNmwncHUTSpVXyOgAfDBqLpnKuJIJZi68rOgJ%2FdDNoEXYBVrSVZ1qOt4lZKHU9MAndXUwVCClkYr%2FSgJaAOrEZd1LbcZnrsqH4oJTV4wpkvqNEYqmORs3dXjUpZUUWWMqlol%2B7uZNzWsNEqlc3TZ0jMEbhsHmkr32cUY1KySdbo28O6Ys1cmXxKWpKQWgm%2FB%2Fux3slX7leKb975hSCNkgCrIcepUtrFPbGeZvkC%2FjoB349umSV1ZLSAHB%2FZerrUiWPHo33TAcO0vSUuIh8FpZYZAEcWdjMf5%2FOnR211IbugIwdY6ZHwUFSe7Iwisai1AY6pgHqYBUb%2FmNSNbi1ptTMMkbe0G%2FT1nRxFiRYHxdL6VUkrYFDUJPOdKPR6Gf7%2FCAt6IwM3ppN%2BePw%2FJeguJyw7XzmAXZF8pOqNRClS1JmPRMLfDYS94ppawuu%2BpazSo1Bq%2BXXbC%2BHtq7fJRZ37cRsuOCFiru02eYcUOrC3IfZ4bJ3NwoAdVvVveR3h2L9EZZbsuuIQiBUOVuufdVgiBG%2BwcWt1V4n46MD&X-Amz-Signature=31b5e60346789f82bc8113c77385797867e4d19dbd5151c5a0b55fb4c476d4d0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It should be **user **`carlos`**’s password!**

Login as carlos with this password

