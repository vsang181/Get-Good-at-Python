# Introducing Conversions

Our fundamental data types include **integers**, **strings**, and **bytes**, with the `bytes` object serving as the primary interface when interacting with low-level system resources. A **character** in Python is simply a string of length one, but conceptually, we often treat it as an atomic unit.

Although we typically work with data in its native form, it is often useful—or even necessary—to **represent that data in another format**. For example, when analysing files, network packets, or memory structures, we commonly work with hexadecimal representations. The same approach applies to binary, octal, and other specialised bases.

Traditionally, Western characters are represented using **one byte (8 bits)**. However, modern computing must support global character sets, including languages such as Arabic, Chinese, and Japanese. These characters typically require **two or more bytes**, forming what is known as **Unicode encoding**.

The main functions and transformations we will use are summarised in the figure below:

<img width="1937" height="397" alt="image" src="https://github.com/user-attachments/assets/d207c1f9-1baf-4695-8228-368dc60bb67c" />
