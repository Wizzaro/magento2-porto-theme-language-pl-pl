# Polish language extension for Magento 2 Porto Theme

## Install

```
composer require wizzaro/magento2-porto-theme-language-pl-pl
```

## Translations for 'Item in Cart' missing in mini cart hack

1. Create file:

```
app/design/frontend/<theme_folder>/<theme_folder>/Magento_Checkout/web/template/cart-items.html
```

For porto theme is:

```
app/design/frontend/Smartwave/porto/Magento_Checkout/web/template/cart-items.html
```

2. Copy content from:

```
vendor/magento/module-checkout/view/web/template/summary/cart-items.html
```

3. Replace:

```html
<div class="title" data-role="title">
    <strong role="heading">
        <translate args="maxCartItemsToDisplay" if="maxCartItemsToDisplay < getCartLineItemsCount()"/>
        <translate args="'of'" if="maxCartItemsToDisplay < getCartLineItemsCount()"/>
        <span data-bind="text: getCartLineItemsCount()"></span>
        <translate args="'Item in Cart'" if="getCartLineItemsCount() === 1"/>
        <translate args="'Items in Cart'" if="getCartLineItemsCount() > 1"/>
    </strong>
</div>
```

to:

```html
<div class="title" data-role="title">
    <strong role="heading"><span data-bind="text: getItemsQty()"></span>
        <!-- ko if: getItemsQty() == 1 -->
        <!-- ko i18n: 'Item in Cart' --><!-- /ko -->
        <!-- /ko -->
        <!-- ko if: getItemsQty() > 1 -->
        <!-- ko i18n: 'Items in Cart' --><!-- /ko -->
        <!-- /ko -->
    </strong>
</div>
```

4. Deploy static content and clear cache