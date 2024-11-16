Common operators like `+`, `-` and `*` works as expected. Only division by `/` operator results always in float. To get integer division we can use functions like `div` or `rem` to get remainder.
```sh
iex(4)> 10/2  
5.0  
iex(5)> div(10, 2)  
5    
iex(7)> rem(10, 3)  
1
```