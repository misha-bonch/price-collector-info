# price-collector

`price-collector` is a research tool that reads public product prices from online shops in Taiwan and Hong Kong
for consumer price statistics. This page explains what it does and how to reach the people who run it.

Its plain HTTP requests identify themselves with this User-Agent:

```
price-collector/1.0 (price statistics research; +https://github.com/misha-bonch/price-collector-info)
```

Pages that only work in a browser are opened in a standard Chrome browser, which sends Chrome's own User-Agent.

## What it collects

- Public prices of a fixed list of everyday products (food, drinks, personal care and similar), as any visitor
  sees them on category and product pages: the current price, a struck "before" price, promotion text and
  availability.
- No personal data. It never signs in, creates an account, places an order or fills a cart.
- It does not use site search.

## How it behaves

- Few requests: at most one request every 5 seconds over plain HTTP, and one page every 15 seconds when a browser
  is needed. A run is bounded; a development check is at most 25 page loads.
- It stops at once on any block, captcha, HTTP 401/403/429 or unexpected redirect, and does not retry that
  day by the same method.
- It does not hide what it is: no rotating IP addresses, no proxy services, no captcha solving, no copied browser
  cookies.
- It prefers the way that needs the fewest requests and puts the least load on a site. Where a shop's own catalogue
  API needs the keys its page gives every anonymous visitor, the collector opens that page once per session, then
  asks the API directly with those keys and its own User-Agent, instead of loading every category page. It never
  signs in and does not reuse the keys after the session.
- It reads each site's robots.txt and records its rules for review; site owners can also tell us directly (see
  Contact).
- Where a shop offers a public data feed or an API its own pages use, that is preferred over loading pages.

## Contact

If you run one of these sites and want us to slow down, change what we read, use a data feed instead, or stop,
please open an issue at **https://github.com/misha-bonch/price-collector-info/issues**. We answer and act on such
requests.

## 中文說明

`price-collector` 是一個用於消費者物價統計研究的工具，讀取台灣及香港網上商店公開顯示的商品價格。
它不收集個人資料，不登入、不下單；請求頻率低（純 HTTP 每 5 秒最多一次，瀏覽器每 15 秒一頁），遇到封鎖或驗證碼即停止。
它盡量以最少的請求讀取資料：如商店自身的商品 API 需要網頁發給匿名訪客的金鑰，工具每次只開啟該網頁一次，之後以這些金鑰及自身的 User-Agent 直接查詢 API，不登入，會話結束後不再使用。
如網站經營者希望我們降低頻率、改用數據源或停止讀取，請在此提交 issue： https://github.com/misha-bonch/price-collector-info/issues
