class.card

```
package com.orbitallpayments.car;

import lombok.Getter;
import lombok.Setter;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import java.io.Serializable;

@Entity
@Getter
@Setter
public class Customer implements Serializable {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private Integer cardNumber;
    private String embossName;
    private String custumerName;
    private String motherName;
    private string address;
    private String city;
}
```

cardservices



```
package com.orbitallpayments.cards.services;
import com.orbitallpayments.cards.domains.cards;
import com.orbitallpayments.cards.repositories.Cards Repository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;
@Service
public class CardService {
    @Autowired
    private cardRepository cardRepository;    public card save(crad card) {
        return cardRepository.save(customer);
    }
    public List<Card> findAll() {
//        return (List<Card>) cardRepository.findAll();
//        List<card> cards = new ArrayList<>();
//        for(Card card : (List<Card>) cardRepository.findAll()) {
//            card.add(card);
//        }
//        return cards;
        List<Card> card = new ArrayList<>();
        cardRepository.findAll().forEach(card :: add);
        return card;
    }
    public Optional<Customer> findById(Long id) {
        return cardRepository.findById(id);
    }
}
```



cardcontroller



```
package com.orbitallpayments.cards.controllers;
import com.orbitallpayments.cards.domains.Customer;
import com.orbitallpayments.cards.services.CardService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.Optional;

@RestController
@RequestMapping("/card")
public class CardController{
    @Autowired
    private  CardService cardService;

    @PostMapping
    public  ResponseEntity<Card> save(@RequestBody Card card) {
        Customer savedCard = cardService.save(card);

        return  new ResponseEntity(savedCard,HttpStatus.CREATED);

    }

    @RequestMapping
    public ResponseEntity<Card> findById(@PathVariable long id){
        Optional<Card> fetchedCustomer = cardService.findById(id);

        return  ResponseEntity.ok(fetchedCard.get());
    }
}
```