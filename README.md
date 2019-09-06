# Static Commerce

Commerce Layer is an API-first platform that lets you transform any plain HTML page into an enterprise-grade e-commerce website, with almost **no coding required**. All you need is to tag HTML pages following some conventions (i.e. class names and SKU codes) and embed Commerce Layer's [official JS library](https://github.com/commercelayer/commercelayer-js). Prices, availability messages, and shopping bag functionalities are automatically mixed into your own content and styling, whatever the CMS, SSG and tools you use to build your site pages.

## 1. Get Your API Credentials

Create a [free developer account](https://core.commercelayer.io/users/sign_up) on Commerce Layer and &mdash; when prompted &mdash; seed it with test data. Navigate to _Settings_ → _Applications_ and take note of the API credentials for your _channel_ application (Client ID, Base endpoint, Allowed scopes). Make sure that **public access is enabled**. The Client secret is not required, as we are building a client side application that would make the secret key visible ([learn more](https://commercelayer.io/api/reference/roles-and-permissions/)).

![Credentials](docs/credentials.png?raw=true "Credentials")

## 2. Configuration

Add an element with `clayer-config` ID and populate its data attributes with your credentials and page preferences. Then add a script link to import the Commerce Layer's JS library right before the closing body tag:

```html
<!DOCTYPE html>
<html>
  <head></head>
  <body>
    <!-- Config -->
    <div
      id="clayer-config"
      data-base-url="https://static-commerce-demo.commercelayer.io"
      data-client-id="377bc0fa1672ef1395fb2113ec187091b2251eefede49ddca761a94adc4ede06"
      data-market-id="418"
      data-country-code="US"
      data-language-code="en"
      data-cart-url="https://example.com/cart"
      data-return-url="https://example.com/return"
      data-privacy-url="https://example.com/privacy"
      data-terms-url="https://example.com/terms"
      data-dev-settings-debug="true"
      data-dev-settings-console="true"
      data-dev-settings-trace="true"
    ></div>

    <!-- JS Library -->
    <script
      type="text/javascript"
      src="https://cdn.jsdelivr.net/npm/commercelayer@1.9.10/dist/commercelayer.min.js"
    ></script>
  </body>
</html>
```

## 3. Static Content

Add any content to the page, like product names, descriptions, and images.

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content -->
    <title>Static Commerce Demo</title>
  </head>
  <body>
    <!-- Static content -->
    <h1>Black Baby Onesie Short Sleeve with Pink Logo (New born)</h1>

    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
      tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim
      veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
      commodo consequat. Duis aute irure dolor in reprehenderit in voluptate
      velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat
      cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id
      est laborum.
    </p>

    <img
      src="https://img.commercelayer.io/skus/BABYONBU000000E63E74NBXX.png?fm=jpg&q=90"
    />

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 4. Prices

Add an element with `clayer-price` class and `data-sku-code` data attribute wherever you want to show a product price. The child element with class `amount` gets populated with the price that has been defined in Commerce Layer for that SKU code, in the current page market ID (see configuration). The child element with class `compare-at-amount` gets populated only if greater than the price amount.

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag -->
    <div class="clayer-price" data-sku-code="BABYONBU000000E63E74NBXX">
      <span class="amount"></span>
      <span class="compare-at-amount"></span>
    </div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 5. Availability Message Templates

Add an element with `clayer-availability-message-available-template` ID as the template tag to be displayed when the selected SKU is available. All the child elements will be automatically populated with the delivery lead time and shipping method information related to the selected variant.

Add an element with `clayer-availability-message-unavailable-template` ID as the template tag to be displayed when the selected SKU is not available. This element will be appended to a specific container when customers will try to add to bag an SKU that is not available (more on this later).

Note that `template` tags are not supported by _IE_ and _Opera Mini_. Use `div` or `span` elements and hide them through CSS if you want to keep legacy browser support.

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message templates-->
    <template id="clayer-availability-message-available-template">
      <p>
        Available in
        <span class="clayer-availability-message-available-min-days"></span>-
        <span class="clayer-availability-message-available-max-days"></span>
        days with
        <span
          class="clayer-availability-message-available-shipping-method-name"
        ></span>
        (<span
          class="clayer-availability-message-available-shipping-method-price"
        ></span
        >)
      </p>
    </template>

    <template id="clayer-availability-message-unavailable-template">
      <p class="has-text-danger">The selected SKU is not available.</p>
    </template>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 6. Add to Bag Buttons

Add a link with `clayer-add-to-bag` class and a list of data attributes as follows:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message templates [...] -->

    <!-- Add to bag button -->

    <a
      href="#"
      class="clayer-add-to-bag"
      data-sku-code="BABYONBU000000E63E74NBXX"
      data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (6 Months)"
      data-sku-reference="Any reference"
      data-sku-image-url="https://img.commercelayer.io/skus/BABYONBU000000E63E74NBXX.png?fm=jpg&q=90&w=400"
      data-availability-message-container-id="availability-message-BABYONBU000000E63E74NBXX"
    >
      Add to bag
    </a>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

The SKU `data-sku-name`, `data-sku-reference`, and `data-sku-image-url` (if present) are used as the line item attributes. The `data-availability-message-container-id` identifies the ID of the element that you want the unavailable messagfe to be appended when the SKU is out of stock. Put the container anywhere in the page:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message templates [...] -->

    <!-- Add to bag button [...] -->

    <!-- Availability message container -->
    <div
      class="clayer-availability-message-container"
      id="availability-message-BABYONBU000000E63E74NBXX"
    ></div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

Sometimes you may want to let the customer add more than one item to the shopping bag. To do that, add an input field with `clayer-add-to-bag-quantity` class and a `data-add-to-bag-quantity-id` data attribute to the add to bag button as follows:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message templates [...] -->

    <!-- Add to bag quantity (optional) -->
    <input
      id="add-to-bag-quantity-BABYONBU000000E63E74NBXX"
      type="number"
      value="1"
      class="clayer-add-to-bag-quantity"
      data-sku-code="BABYONBU000000E63E74NBXX"
    />

    <!-- Add to bag button (with optional quantity identifier)-->
    <a
      href="#"
      class="clayer-add-to-bag"
      data-sku-code="BABYONBU000000E63E74NBXX"
      data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (6 Months)"
      data-sku-reference="Any reference"
      data-sku-image-url="https://img.commercelayer.io/skus/BABYONBU000000E63E74NBXX.png?fm=jpg&q=90&w=400"
      data-availability-message-container-id="availability-message-BABYONBU000000E63E74NBXX"
      data-add-to-bag-quantity-id="add-to-bag-quantity-BABYONBU000000E63E74NBXX"
    >
      Add to bag
    </a>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 7. Variant Options

If your product has many variants, add an element with `clayer-variant` class and `data-sku-code` for each variant option. You can use either a `select` tag or a list of `radio` buttons. The list if data attributes that you can add to each option are the same of the shopping bag example above. The add to bag button is not referred to a specific SKU and its data attributes get updated when an option is selected. You can optionally add a quantity field to let the customer add more than one item to the shopping bag.

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message templates [...] -->

    <!-- Variants (select, with optional quantity identifier) -->
    <select
      class="clayer-variant-select"
      name="variant"
      data-availability-message-container-id="availability-message"
      data-add-to-bag-id="add-to-bag"
      data-add-to-bag-quantity-id="add-to-bag-quantity"
    >
      <option value="" disabled selected>Select variant</option>
      <option
        class="clayer-variant"
        data-sku-code="BABYONBU000000E63E74NBXX"
        data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (New born)"
        >New born</option
      >
      <option
        class="clayer-variant"
        data-sku-code="BABYONBU000000E63E746MXX"
        data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (6 Months)"
        >6 months</option
      >
      <option
        class="clayer-variant"
        data-sku-code="BABYONBU000000E63E7412MX"
        data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (12 Months)"
        >12 Months</option
      >
    </select>

    <!-- Add to bag quantity (optional) -->
    <input
      id="add-to-bag-quantity"
      type="number"
      value="1"
      class="clayer-add-to-bag-quantity"
    />

    <!-- Add to bag -->

    <!-- Variants (radio, with optional quantity identifier) -->
    <!-- <input class="clayer-variant clayer-variant-radio" name="variant" type="radio"
           data-sku-code="BABYONBU000000E63E74NBXX"
           data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (New born)"
           data-sku-reference="Commerce Layer 01"
           data-sku-image-url="https://img.commercelayer.io/skus/BABYONBU000000E63E74.png?fm=jpg&q=90"
           data-price-container-id="price"
           data-availability-message-container-id="availability-message"
           data-add-to-bag-id="add-to-bag"
           data-add-to-bag-quantity-id="add-to-bag-quantity" /> New born

    <input class="clayer-variant clayer-variant-radio" name="variant" type="radio"
           data-sku-code="BABYONBU000000E63E746MXXFAKE"
           data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (6 Months)"
           data-sku-reference="Commerce Layer 01"
           data-sku-image-url="https://img.commercelayer.io/skus/BABYONBU000000E63E74.png?fm=jpg&q=90"
           data-price-container-id="price"
           data-availability-message-container-id="availability-message"
           data-add-to-bag-id="add-to-bag"
           data-add-to-bag-quantity-id="add-to-bag-quantity" /> 6 months

    <input class="clayer-variant clayer-variant-radio" name="variant" type="radio"
           data-sku-code="BABYONBU000000E63E7412MX"
           data-sku-name="Black Baby Onesie Short Sleeve with Pink Logo (12 Months)"
           data-sku-reference="Commerce Layer 01"
           data-sku-image-url="https://img.commercelayer.io/skus/BABYONBU000000E63E74.png?fm=jpg&q=90"
           data-price-container-id="price"
           data-availability-message-container-id="availability-message"
           data-add-to-bag-id="add-to-bag"
           data-add-to-bag-quantity-id="add-to-bag-quantity" /> 12 Months -->

    <!-- Add to bag button -->
    <a
      href="#"
      class="clayer-add-to-bag"
      id="add-to-bag"
      data-availability-message-container-id="availability-message"
      >Add to bag</a
    >

    <!-- Availability message container -->
    <div
      class="clayer-availability-message-container"
      id="availability-message"
    ></div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 8. Shopping Bag

Add an element with `clayer-shopping-bag-container` ID wherever you want to show the shopping bag.

The `clayer-shopping-bag-items-container` is used as the parent element of the shopping bag line items, built from the `clayer-shopping-bag-item-template` template tag.

Add the summary elements wherever you want to show the current shopping bag details. The `clayer-shopping-bag-toggle` element toggles an `open` class on the shopping bag container.

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message templates [...] -->

    <!-- Variant options [...] -->

    <!-- Add to bag button [...] -->

    <!-- Availability message container [...] -->

    <!-- Shopping Bag -->
    Your shopping bag contains <span class="clayer-shopping-bag-items-count">0</span> items (<span class="clayer-shopping-bag-total"></span>) <a href="#" class="clayer-shopping-bag-toggle">toggle</a>

    <div id="clayer-shopping-bag-container">
      <table class="table is-fullwidth">
        <thead>
          <tr>
            <th colspan="2">SKU</th>
            <th>Reference</th>
            <th>Unit price</th>
            <th>Q.ty</th>
            <th>Total</th>
            <th></th>
          </tr>
        </thead>
        <tbody id="clayer-shopping-bag-items-container">
        </tbody>
        <template id="clayer-shopping-bag-item-template">
          <tr>
            <td>
              <img class="clayer-shopping-bag-item-image"></img>
            </td>
            <td class="clayer-shopping-bag-item-name"></td>
            <td class="clayer-shopping-bag-item-reference"></td>
            <td class="clayer-shopping-bag-item-unit-amount"></td>
            <td class="clayer-shopping-bag-item-qty-container">
              <!-- The unavailable message template is appended to the element
                    below if customer selects a quantity that is not available  -->
              <span class="clayer-shopping-bag-item-availability-message-container"></span>
            </td>
            <td class="clayer-shopping-bag-item-total-amount"></td>
            <td>
              <a href="#" class="clayer-shopping-bag-item-remove">remove</a>
            </td>
          </tr>
        </template>
      </table>

      <table class="table is-fullwidth">
        <tr>
          <td>Subtotal</td>
          <td class="clayer-shopping-bag-subtotal"></td>
        </tr>
        <tr>
          <td>Shipping</td>
          <td class="clayer-shopping-bag-shipping"></td>
        </tr>
        <tr>
          <td>Payment</td>
          <td class="clayer-shopping-bag-payment"></td>
        </tr>
        <tr>
          <td>Discount</td>
          <td class="clayer-shopping-bag-discount"></td>
        </tr>
        <tr>
          <td>Taxes</td>
          <td class="clayer-shopping-bag-taxes"></td>
        </tr>
        <tr>
          <td>Total</td>
          <td class="clayer-shopping-bag-total"></td>
        </tr>
      </table>
    </div>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 9. Checkout Button

Add an element with `clayer-shopping-bag-checkout` class wherever you want to show the checkout button. The customer will be redirected to the Commerce Layer's hosted checkout application to complete the purchase and place the order.

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Static content [...] -->
  </head>
  <body>
    <!-- Static content [...] -->

    <!-- Price tag  [...] -->

    <!-- Variants [...] -->

    <!-- Availability message templates [...] -->

    <!-- Variant options [...] -->

    <!-- Add to bag button [...] -->

    <!-- Availability message container [...] -->

    <!-- Shopping Bag [...] -->

    <!-- Checkout button -->
    <a href="#" class="clayer-shopping-bag-checkout">Proceed to checkout</a>

    <!-- Config [...] -->

    <!-- JS Library [...] -->
  </body>
</html>
```

## 10. Document events

Commerce Layer library dispatches the following document events:

| Event name               | Description                          |
| ------------------------ | ------------------------------------ |
| clayer-prices-ready      | Prices have been updated             |
| clayer-variants-ready    | Variants have been updated           |
| clayer-add-to-bags-ready | Add to bag buttons have been updated |
| clayer-variant-selected  | SKU has been selected                |
| clayer-line-item-created | SKU has been added to bag            |
| clayer-line-item-updated | Line item quantity has been changed  |
| clayer-line-item-deleted | Line item has been removed from cart |
| clayer-order-ready       | Order (cart) has been fetched        |

## 11. Custom checkout, customer accounts, and more

For some clients, you may want to build your own checkout experience, rather than redirecting customers to the hosted checkout application provided by Commerce Layer. Another common feature that you may want to build is a customer account area, where they can manage their order history, wallet (i.e. saved payment methods), address book and returns.

The next versions of Commerce Layer's JS library will be enhanced to provide all those features with equal ease. In the meantime, please explore the official [API reference](https://commercelayer.io/api/reference/) for all the available endpoints and resources.
