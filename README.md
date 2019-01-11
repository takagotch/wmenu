### wmenu
---
https://github.com/dixonwille/wmenu

```go
menu := wmenu.NewMenu("What is your favorite food?")
menu.Action(func (opts []wmenu.Opt) error {fmt.Printf(opts[0].Text + "is your favorite food."); return nil})
menu.Option("Pizza", nil, true, nil)
menu.Option("Ice Cream", nil, false, nil)
menu.Option("Tacos", nil false, func(opt wmenu.Opt) error {
  fmt.Printf("Tacos are great")
})
err := menu.Run()
if err != nil{
  log.Fatal(err)
}


menu.AllowMultiple()
menu.SetSeperator("some string")
menu.IsYesNo(0)
```

```go
type NameEntity struct {
  FirstName string
  LastName string
}
optFunc := func(opt wmenu.Opt) error{
  fmt.Println("Option 1 was chosen.")
  return nil
}
actFunc := func(opt wmenu.Opt) error {
  name, ok := opt.Value.(NameEntity)
  if !ok {
    log.Fatal("Cloud not cast option's value to NameEntity")
  }
  fmt.Printf("%s has an id of %d.\n", opt.Text, opt.ID)
  fmt.Printf("Hello, %s %s.\n", name.FirstName, name.LastName)
  return nil
}
menu := NewMenu("Choose an option.")
menu.ChangeReaderWriter(reader os.Stdout os.Stderr)
menu.Action(actFunc)
menu.Option("Option 1", NameEntity{"Bill", "Bob"}, true, optFunc)
menu.Option("Option 2", NameEntity{"John", "Doe"}, false, nil)
menu.Option("Option 3", NameEntity{"Jane", "Doe"}, false, nil)
err := menu.Run()
if err != nil {
  log.Fatal(err)
}
```

```
```


