# Software Testing (Black Box) for Facebook.com

Black box testing using different tools for the Facebook website to find bugs and make test cases.

---

White box testing techniques analyse the internal structures the used data structures, internal design, code structure and the working of the software rather than just the functionality as in black box testing. It is also called glass box testing or clear box testing or structural testing.

Since we do not have access to the code of Facebook, we are only conducting black box (functionality) testing.

---

### Dirsearch

```bash
git clone https://github.com/maurosoria/dirsearch.git
cd dirsearch 
python3 dirsearch.py -u https://facebook.com -e js,html
```

**OUTPUT:** Output File: `/Users/akshatvg/Desktop/ST/dirsearch/reports/facebook.com/_21-12-03_01-27-15.txt`


### Findomain

```bash
brew install findomain
findomain -qt facebook.com > findomain.txt
```

### Unimap

```bash
git clone https://github.com/Edu4rdSHL/unimap && cd unimap
cargo build --release
cd target/release
sudo unimap --fast-scan -f ../../../findomain.txt
```

**NOTE:** It will take a lot of time for this because number of subdomains that we got are in lakhs.

### ffug- parameter fuzzing using brute force

```bash
git clone https://github.com/ffuf/ffuf && cd ffuf && go get && go build
ffuf -w ../findomain.txt -u https://facebook.com/ -H "Host: FUZZ" -mc 200 > ffuf_response.txt
ffuf -w ../findomain.txt -u https://facebook.com/ -H "Host: FUZZ" -mc 400 > ffuf_response_400.txt
```

### Future Scope

- Rate limiting: Vegeta to send 100 requests for login to test if the APIs rate limit a user.
- Stress testing: K6 to check with thousands of users. The servers should auto-scale.