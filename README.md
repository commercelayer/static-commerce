# Static Commerce Demo

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

## 1. Get your credentials

Create a [free developer account](https://core.commercelayer.io/users/sign_up) on Commerce Layer and &mdash; when prompted &mdash; seed it with test data. Navigate to _Settings_ → _Applications_ and take note of the API credentials for your _channel_ application (Client ID, Base endpoint, Allowed scopes). Make sure that **public access is enabled**. The Client secret is not required, as we are building a client side application that would make the secret key visible ([learn more](https://commercelayer.io/api/reference/roles-and-permissions/)).

![Credentials](docs/credentials.png?raw=true "Credentials")

## 2. Configure your site

``` html
<!DOCTYPE html>
<html>
  <head></head>
  <body>

    <!-- Config -->
    <div id="clayer-config"
      data-base-url="https://static-commerce.commercelayer.io"
      data-client-id="351020e9c84f2076755083f08bfe8e47365a76395db1059c3219c37abff86534"
      data-market-id="185"
      data-country-code="US"
      data-language-code="en"
      data-cart-url="http://example.com/cart"
      data-return-url="http://example.com/return"
      data-privacy-url="http://example.com/privacy"
      data-terms-url="http://example.com/terms">
    </div>

    <!-- JS Library -->
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/commercelayer@1.2.1/dist/commercelayer.min.js"></script>
  </body>
</html>
```

## 3. Add static content

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content -->  
    <title>Static Commerce Demo</title>
  </head>
  <body>

    <!-- Static content -->
    <h1>Black Men T-shirt with White Logo</h1>
    <img src="https://img.commercelayer.io/skus/TSHIRTMM000000FFFFFF.png?fm=jpg&q=90" />

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 4. Add price(s)

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->    
  </head>
  <body>

    <!-- Static content [...] -->    

    <!-- Price tag -->
    <div class="clayer-price" data-sku-code="TSHIRTMM000000FFFFFFMXXX">
      <span class="amount"></span>
      <span class="compare-at-amount"></span>
    </div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 5. Add variant options

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->    
  </head>
  <body>

    <!-- Static content [...] -->    

    <!-- Price tag  [...] -->

    <!-- Variants -->
    <input class="clayer-variant" type="radio" data-sku-code="TSHIRTMM000000FFFFFFMXXX" data-sku-name="Black Men T-shirt with White Logo (M)" name="variant" /> M
    <input class="clayer-variant" type="radio" data-sku-code="TSHIRTMM000000FFFFFFLXXX" data-sku-name="Black Men T-shirt with White Logo (L)" name="variant" /> L
    <input class="clayer-variant" type="radio" data-sku-code="TSHIRTMM000000FFFFFFXLXX" data-sku-name="Black Men T-shirt with White Logo (XL)" name="variant" /> XL

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 6. Add availability message

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->    
  </head>
  <body>

    <!-- Static content [...] -->    

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message -->
    <div id="clayer-availability-message-container">
      <template id="clayer-availability-message-available-template">
        <p>
          Available in
          <span class="clayer-availability-message-available-min-days"></span>-
          <span class="clayer-availability-message-available-max-days"></span> days with
          <span class="clayer-availability-message-available-shipping-method-name"></span>
          (<span class="clayer-availability-message-available-shipping-method-price"></span>)
        </p>
      </template>
      <template id="clayer-availability-message-unavailable-template">
        <p>The selected SKU is not available.</p>
      </template>
    </div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 7. Add to bag button

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->    
  </head>
  <body>

    <!-- Static content [...] -->    

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message [...] -->

    <!-- Add to bag -->
    <a href="#" class="clayer-add-to-bag">Add to shopping bag</a>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 8. Add shopping bag

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->    
  </head>
  <body>

    <!-- Static content [...] -->    

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message [...] -->

    <!-- Add to bag [...] -->

    <!-- Shopping bag -->
    <span id="clayer-shopping-bag-items-count">0</span>
    <a href="#" id="clayer-shopping-bag-toggle">toggle shopping bag</a>

    <div id="clayer-shopping-bag-container">
      <div id="clayer-shopping-bag-items-container">

        <!-- Line item template -->
        <template id="clayer-shopping-bag-item-template">
          <img class="clayer-shopping-bag-item-image"></img>
          <div class="clayer-shopping-bag-item-name"></div>
          <div class="clayer-shopping-bag-item-unit-amount"></div>
          <div class="clayer-shopping-bag-item-qty-container"></div>
          <div class="clayer-shopping-bag-item-total-amount"></div>
          <a href="#" class="clayer-shopping-bag-item-remove">remove</a>
        </template>

        <!-- Summary -->
        <div id="clayer-shopping-bag-subtotal"></div>
        <div id="clayer-shopping-bag-shipping"></div>
        <div id="clayer-shopping-bag-payment"></div>
        <div id="clayer-shopping-bag-discount"></div>
        <div id="clayer-shopping-bag-taxes"></div>
        <div id="clayer-shopping-bag-total"></div>
      </div>
    </div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 9. Add checkout button

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->    
  </head>
  <body>

    <!-- Static content [...] -->    

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message [...] -->

    <!-- Add to bag [...] -->

    <!-- Shopping bag [...] -->

    <a href="#" id="clayer-shopping-bag-checkout">Proceed to checkout</a>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 10. What's next?

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

<!-- <input class="clayer-variant" name="variant" type="hidden" data-sku-code="TSHIRTMMFFFFFF000000LXXX" data-sku-name="White Men T-shirt with Black Logo (XL)" /> -->

<!-- <select class="clayer-variant-select">
  <option class="clayer-variant" data-sku-code="TSHIRTMM000000FFFFFFXLXX" data-sku-name="Black Men T-shirt with White Logo (XL)">Black Men T-shirt with White Logo (XL)</option>
  <option class="clayer-variant" data-sku-code="TSHIRTMMFFFFFF000000LXXX" data-sku-name="White Men T-shirt with Black Logo (L)">White Men T-shirt with Black Logo (L)</option>
</select> -->
