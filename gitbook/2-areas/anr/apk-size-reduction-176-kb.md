some more context: This library was added when there was requirement to check validation of international phone numbers. This lib internally stores the valid format structures for different country codes (Indonesia and others) in .proto files. I did an experiment few weeks back to include the source code of the library rather than the binary format and did clean up of the unneeded .proto files. We were able to reduce the apk size by 176KB. 

But we didn't release it as it was not worth the effort. When push comes to shove, we may merge the changes. 

If you are planning to add this library now, I would suggest to look into alternative lite-weight contenders.

PR - [Page not found · GitHub · GitHub](https://github.com/Meesho/supply_android/pull/7711)

