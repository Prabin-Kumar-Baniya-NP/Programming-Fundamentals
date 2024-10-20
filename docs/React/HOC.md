# Higher Order Components

- It takes a component and returns a component.

```js
const RestaurantCard = () => {
  return <>JSX</>;
};

const withPromotedLablel = (RestaurantCard) => {
  return (props) => {
    return (
      <div>
        <label>Promoted</label>
        <Restaurantcard {...props} />
      </div>
    );
  };
};

const PromotedRestaurantCard = withPromotedLablel(RestaurantCard);
```

- Controlled vs Uncontrolled Component: If a component behaviour is controlled by its own state variables then its a uncontrolled component. But if some other component is passing some values to a component due to which that component behaviour changes, then its a controlled component.