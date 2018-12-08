=====
Usage
=====

An example should be enough::

    import re
    from reagex import reagex

    # Just a bad example (italian address pattern)
    pattern = reagex(
        '{_address} {postcode} {city} {province}',
        # groups starting with "_" are non-capturing
        _address = reagex(
            '{street} {number}',
            street = '(via|contrada|c/da|c.da|piazza|p.za) [a-zA-Z]+',
            number = 'snc|[0-9]+'
        ),
        postcode = '[0-9]{5}',
        city = '[A-Za-z]+',
        province = '[A-Z]{2}'
    )

    matcher = re.compile(pattern)
    match = matcher.fullmatch('via Roma 123 12345 Napoli NA')
    print(match.groupdict())
    # prints:
    #   {'city': 'Napoli',
    #    'number': '123',
    #    'postcode': '12345',
    #    'province': 'NA',
    #    'street': 'via Roma'}

