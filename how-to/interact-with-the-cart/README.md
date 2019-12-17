# How to Interact with the Cart

Some of your custom blocks may need to interact with the cart, for example if you wanted to add an item to the cart from your block, or trigger an action in your block after a shopper adds an item to the cart. You can do this with the included PubSubJS mechanism.

## 1. Listening for a Cart Event

If you want your block to respond to changes in the cart, you should set up your block to listen for a cart event using PubSubJS.

### Add a Subscription in Your Block's componentDidMount Function

Locate the `componentDidMount` function of one of your blocks. If this function doesn't exist yet, add it to your component. You may need to refactor the block to use class syntax. Then add a subscription:

```js
componentDidMount() {
    this.props.pubSub.subscribe(
        this.props.events.cart.itemAddedToCart, // must match one of the cart events
        this.handleItemAdded
    );
}
```

`utils.pubSub.subscribe()` takes two arguments:

1. A topic name, which should be one of the [Cart Events](/references/cart-events/README.md).
2. A handler function. The message will be passed to the handler function.

### Implement Your Handler Function for the Subscription

Your handler function is the code that actually does something with the data received from the cart event. Add it to your block component as an instance property.

```js
// inside the body of your component
handleItemAdded = (msg, itemData) => {
    // do something with itemData. In this example we will set it to state.
    this.setState({ itemAdded: itemData });
};
```

## 2. Publishing an Event to the Cart

Your block may want to publish an event to the cart. This can allow you to add an item, update an item count, or open the cart panel. In this example, we'll add an item to the cart.

### Ensuring That the Cart Is Loaded

Before you publish any events to the cart, you should be aware that under some circumstances, the cart may not have loaded yet. For example, if you are adding something to the cart based on a query string parameter, not a user interaction. In that case, you may want to verify that the cart is loaded before you publish an event to the cart:

```js
// you can use this function to ask the cart if it's loaded yet.
// you can also run this function on an interval until the cart responds.
this.props.pubSub.publish(this.props.events.cart.askIfLoaded, {});

// the cart will respond to the cart.askIfLoaded event by publishing a cart.replyWithLoaded event.
// You can subscribe to like so:
this.props.pubSub.subscribe(this.props.events.cart.replyWithLoaded, this.handleCartLoaded);

// define a handler function that will run after the cart loads
handleCartLoaded = (msg, data) => {
    // the cart has loaded and you can now interact with it
}
```

### Add a Function to Send Your Message

Send your message using `utils.pubSub.publish()` in your block. This function takes two arguments:

1. A topic name, which should be one of the [Cart Events](/references/cart-events/README.md). The cart block will listen for this topic.
2. A data value (any type). This is the piece of data you will send to the cart.

Example:

```js
// in your block component body, add a function. Here we're doing it as an instance property because this component is a class.
addItem = itemData => {
    this.props.pubSub.publish(this.props.events.cart.addToCart, itemData);
};
```

Note: if your component is a stateless functional component rather than an ES6 class, you would define your function as a const rather than an instance property.

In this example, the cart block expects `itemData` to be an object with the following properties:

```js
{
    productId,
    quantity,
    variantId,
    itemPrice
}
```

## Further Reading

To get a sense of what cart interactions are possible, see the [Cart Events Reference](/references/cart-events/README.md).

For more details on PubSubJS, see the [PubSubJS npm reference](https://www.npmjs.com/package/pubsub-js).
