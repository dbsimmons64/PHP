N.B. A transaction is not a lock.

```php
DB::transaction(function () use ($unit_price) {
    $player = Player::where('id',$player_id)->lockForUpdate()->first();

    if($player->gold >= $unit_price && $player->has_purchased == false){
        $player->has_purchased = true;
        $player->gold -= $unit_price;
        $player->save();
    
        $unit = new Unit();
        $unit->player_id = $player->id;
        $unit->save();
    }
});
```

Note the `lockforUpdate`.