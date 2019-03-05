# Static Commerce

Commerce Layer is an API-first platform that lets you transform any plain HTML page into an enterprise-grade e-commerce website, with **no coding required**. All you need is to tag your HTML pages following some conventions (i.e. class names and SKU codes) and embed Commerce Layer's official JS library. Prices, availability messages, and shopping bag functionalities will be automatically mixed into your own content and styling, whatever the CMS, SSG and tools you use to build your website.

## 1. Get Your API Credentials

Create a [free developer account](https://core.commercelayer.io/users/sign_up) on Commerce Layer and &mdash; when prompted &mdash; seed it with test data. Navigate to _Settings_ → _Applications_ and take note of the API credentials for your _channel_ application (Client ID, Base endpoint, Allowed scopes). Make sure that **public access is enabled**. The Client secret is not required, as we are building a client side application that would make the secret key visible ([learn more](https://commercelayer.io/api/reference/roles-and-permissions/)).

![Credentials](docs/credentials.png?raw=true "Credentials")

## 2. Add Configuration

Add an element with `clayer-config` ID and populate its data attributes with your credentials and page preferences. Then add a script link to import the Commerce Layer's JS library right before the closing body tag:

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
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/commercelayer@1.8.0/dist/commercelayer.min.js"></script>
  </body>
</html>
```

## 3. Add Static Content

Add any content to the page, like product names, descriptions, and images.

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

    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>

    <img src="https://img.commercelayer.io/skus/TSHIRTMM000000FFFFFF.png?fm=jpg&q=90" />

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 4. Add Prices

Add an element with `clayer-price` class and `data-sku-code` data attribute wherever you want to show a product price. The child element with class `amount` will be populated with the price that has been defined for the parent SKU code, scoped to the current page market ID (see configuration). The child element with class `compare-at-amount` will be populated only if greater than the price amount.

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

## 5. Add Variant Options

Add an element with `clayer-variant` class and `data-sku-code` data attribute wherever you want to show a variant option. You can use either a `select` tag with class `clayer-variant-select` or a list of `radio` buttons. Use a hidden field when the product has no variants. The first variant is automatically selected on page load.

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

    <!-- Option 1: Select -->

    <select class="clayer-variant-select">
      <option class="clayer-variant" data-sku-code="TSHIRTMM000000FFFFFFXLXX" data-sku-name="Black Men T-shirt with White Logo (XL)">Black Men T-shirt with White Logo (XL)</option>
      <option class="clayer-variant" data-sku-code="TSHIRTMMFFFFFF000000LXXX" data-sku-name="White Men T-shirt with Black Logo (L)">White Men T-shirt with Black Logo (L)</option>
    </select>

    <!-- Option 2: Radio buttons -->

    <!-- <input class="clayer-variant" type="radio" data-sku-code="TSHIRTMM000000FFFFFFMXXX" data-sku-name="Black Men T-shirt with White Logo (M)" name="variant" /> M
    <input class="clayer-variant" type="radio" data-sku-code="TSHIRTMM000000FFFFFFLXXX" data-sku-name="Black Men T-shirt with White Logo (L)" name="variant" /> L
    <input class="clayer-variant" type="radio" data-sku-code="TSHIRTMM000000FFFFFFXLXX" data-sku-name="Black Men T-shirt with White Logo (XL)" name="variant" /> XL -->

    <!-- Option 3: Hidden field (no variants) -->

    <!-- <input class="clayer-variant" name="variant" type="hidden" data-sku-code="TSHIRTMMFFFFFF000000LXXX" data-sku-name="White Men T-shirt with Black Logo (XL)" /> -->

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 6. Add Availability Messages

Add an element with `clayer-availability-message-container` ID wherever you want to show the availability message of the selected variant.

Add an element with `clayer-availability-message-available-template` ID as the template tag to be used when the selected SKU is available. The child elements will be automatically populated with the delivery lead time and shipping method information.

Add an element with `clayer-availability-message-unavailable-template` ID as the template tag to be used when the selected SKU is not available.

Note that `template` tags are not supported by _IE_ and _Opera Mini_. Use `div` or `span` elements and hide them through CSS if you want to keep legacy browser support.

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
    </div>
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

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 7. Add Buy Button

Add an element with `clayer-add-to-bag` class wherever you want to show the add to bag button. The library binds a function to the _click_ event, so that the selected variant is added to the shopping bag. The library adds a `disabled` class to the element whenever an unavailable SKU is selected.

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

    <!-- Add to bag (multiple) -->
    <!-- <a href="#" class="clayer-add-to-bag" data-sku-code="TSHIRTMM000000FFFFFFMXXX">Add to shopping bag</a> -->
    <!-- <a href="#" class="clayer-add-to-bag" data-sku-code="TSHIRTMM000000FFFFFFLXXX">Add to shopping bag</a> -->
    <!-- <a href="#" class="clayer-add-to-bag" data-sku-code="TSHIRTMM000000FFFFFFXLXX">Add to shopping bag</a> -->

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 8. Add Shopping Bag

Add an element with `clayer-shopping-bag-container` ID wherever you want to show the shopping bag.

The `clayer-shopping-bag-items-container` will be used as the parent element of the shopping bag line items, automatically built from the `clayer-shopping-bag-item-template` template tag.

Add the summary elements wherever you want to show the current shopping bag details. The `clayer-shopping-bag-toggle` element will toggle an `open` class on the shopping bag container.

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
      </div>

      <!-- Line item template -->
      <template id="clayer-shopping-bag-item-template">
        <div><!-- Make sure to wrap the the line item elements -->
          <img class="clayer-shopping-bag-item-image"></img>
          <div class="clayer-shopping-bag-item-name"></div>
          <div class="clayer-shopping-bag-item-unit-amount"></div>
          <div class="clayer-shopping-bag-item-qty-container"></div>
          <div class="clayer-shopping-bag-item-total-amount"></div>
          <a href="#" class="clayer-shopping-bag-item-remove">remove</a>          
        </div>
      </template>      

      <!-- Summary -->
      <div id="clayer-shopping-bag-subtotal"></div>
      <div id="clayer-shopping-bag-shipping"></div>
      <div id="clayer-shopping-bag-payment"></div>
      <div id="clayer-shopping-bag-discount"></div>
      <div id="clayer-shopping-bag-taxes"></div>
      <div id="clayer-shopping-bag-total"></div>

    </div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 9. Add Checkout Button

Add an element with `clayer-shopping-bag-checkout` ID wherever you want to show the checkout button. The customer will be redirected to the Commerce Layer's hosted checkout application to complete the purchase and place the order.

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

## 10. Custom checkout, customer accounts, and more

For some clients, you may want to build your own checkout experience, rather than redirecting customers to the hosted checkout application provided by Commerce Layer. Another common feature that you may want to build is a customer account area, where they can manage their order history, wallet (i.e. saved payment methods), address book and returns.

The next versions of Commerce Layer's JS library will be enhanced to provide all those features with equal ease. In the meantime, please explore the official [API reference](https://commercelayer.io/api/reference/) for all the available endpoints and resources.
