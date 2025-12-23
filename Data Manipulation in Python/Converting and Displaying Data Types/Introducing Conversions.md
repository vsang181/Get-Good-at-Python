# Introducing Conversions

Our basic data types are integers and strings and the bytes object is used when interacting with the underlying system. Characters are a special atomic string.

We will use data objects in their native forms and represent them as native strings, but we may also want to represent them in another form. We will learn how tob work with various data types in hexadecimal and we can take a similar approach for binary, octal or any other exotic base.

Characters in their "western" form are represented as 8 bits - a single byte. However because computers support more complex languages such as Arabic and Japanese, the representation of characters often uses two bytes. This is known as the Unicode form.

Let us review hwo we move form one data object form to another and how we betwenn displayable strings. The funcations we will use are summarised in the figure below.

<img width="1937" height="397" alt="image" src="https://github.com/user-attachments/assets/d207c1f9-1baf-4695-8228-368dc60bb67c" />

