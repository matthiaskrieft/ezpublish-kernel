# Content download

> Author: bd@ez.no

## Summary
This feature covers downloading of Content binary files over HTTP.

It covers:
- generation of proper links from Twig as well as PHP,
- permissions checking (the user must be allowed to read the Content)
- streaming of the file over HTTP

## Components

### Twig helper

> Name: ez_download_path
> Usage: `ez_download_path( content, 'file' )`

The helper will be used to generate a download link for a given Field/Content.

### Controller action + route

> Route: `/content/download/{fileId}/{fileName}`

The controller action will load the content based on the fileId. Usual permissions checking will occur at that time.
The binary file referenced by the Field Value will then be streamed, using the active IO Service.

It *should* also support HTTP caching, by making sure the proper headers are sent.

It *could* support resuming (a *must* for media files).

### Download service

Used by both the twig helper and the controller, the service can also be used by developers to generate a download link.

## Options

### IgorwFileServeBundle

> https://github.com/igorw/IgorwFileServeBundle

A package meant to replace the BinaryResponse we currently use. Supports server-side mechanism such as X-SendFile, but
seems to be stalled a bit.
