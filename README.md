# kotlin-samples
This is a sample repo to show how Kotlin DSL help in adding values to our projects. DL simplifies code plus helps in generalising solutions. Currently this repo contains solutions for Android specific APIs only but anyone is free to add and suggest any DSL that can benefit the others. I have a dsl package in all my recent projects where i have added some DSLs that i now use regularly one specifically related to Dialogs.


### Alert Dialog
This example shows how to create default Alert Dialog DSL. It's mostly a buildup to next examples.

```
    alert {
          title = "Hey Title"
          description = "Hey Description"
          alertContext = context
          positiveButton = {
              Toast.makeText(context, "Yes", Toast.LENGTH_LONG).show()
          }

          negativeButton = {
              Toast.makeText(context, "And No", Toast.LENGTH_LONG).show()
          }
     }
```        

### Alert Dialog with CustomView
This example shows how to create custom Alert Dialogs. We can pass any **layoutId** here then in setCustomView we can set views data and implement callbacks. Though use of **findViewById** use here feels annoying since we have got kotlin android extensions now. Anyway don't worry we'll fix that.

```
    val alertData = AlertData(
                    "This is a Custom Dialog Title",
                    "This is a Custom Dialog Description"
            )
      customAlert {

          layoutId = R.layout.layout_dialog
          setCustomView = { it: View, dialog: AlertDialog ->

              it.findViewById<TextView>(R.id.title).text = alertData.title
              it.findViewById<TextView>(R.id.description).text = alertData.description

              it.findViewById<TextView>(R.id.accept).setOnClickListener {
                  Toast.makeText(context, "accept button click", Toast.LENGTH_LONG).show()
                  dialog.dismiss()
              }

              it.findViewById<TextView>(R.id.reject).setOnClickListener {
                  Toast.makeText(context, "reject button click", Toast.LENGTH_LONG).show()
                  dialog.dismiss()
              }

          }
      }
```    

### Dialog using Dialog Fragment
This example shows how to create dialog just pass any **layoutId** and then in setCustomView set data or implement callbacks BTW here you don't have to use **findViewById** anymore. Now making dialogs in Android not only becomes easy but beautiful.

```
      dialog {
          layoutId = R.layout.layout_dialog
          setCustomView = {
              it.title.text = getString(R.string.fragment_dialog_title)
              it.description.text = getString(R.string.fragment_dialog_description)

              it.accept.setOnClickListener {
                  Toast.makeText(context, "accept button click", Toast.LENGTH_LONG).show()
              }

              it.reject.setOnClickListener {
                  Toast.makeText(context, "reject button click", Toast.LENGTH_LONG).show()
              }

          }
      }
```    

### Bottom sheet Dialog using BottomSheetDialogFragment
Just like Dialog fragment we can create DSL for BottomSheetDialog fragment or any other similar use cases.
```
      bottomSheetDialog {
          layoutId = R.layout.layout_dialog
          setCustomView = {
              it.title.text = getString(R.string.fragment_dialog_title)
              it.description.text = getString(R.string.fragment_dialog_description)

              it.accept.setOnClickListener {
                  Toast.makeText(context, "accept button click", Toast.LENGTH_LONG).show()
              }

              it.reject.setOnClickListener {
                  Toast.makeText(context, "reject button click", Toast.LENGTH_LONG).show()
              }

          }
      }

```   


### Request DSL permission using DSL
This is a basic example to show how it can be so easy to ask permission in Android using below DSL. You can use this example as it is if you only require one permission oe more than one permission you can add your implementation in PermissionActivity class.
```
      val permissionsList = arrayOf(
              Manifest.permission.WRITE_EXTERNAL_STORAGE
      )

      getPermissions {
          permissions = permissionsList
          onPermissionGranted = {
              Toast.makeText(context, "Permission Given", Toast.LENGTH_LONG).show()
          }

          onPermissionDenied = {
              Toast.makeText(context, "Permission Denied", Toast.LENGTH_LONG).show()
          }
      }
  }
```    
