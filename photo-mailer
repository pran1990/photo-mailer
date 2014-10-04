#!/usr/bin/env python
import argparse
import imghdr
import os
import sys


class MadnessException(Exception):
    def __init__(self, msg):
        m = 'This is madness!!\n' + msg
        print(msg)

def parse():
    parser = argparse.ArgumentParser(description='photo-mailer')
    parser.add_argument('-d', '--dryrun', action='store_true',
                        help='Really mail out photos')
    parser.add_argument('-c', '--count', action='store', default=1,
                        help='How many photos per day')

    # NOTE(praneshp): an enterprising boyfriend can add code here
    # to pick up photos from somewhere else, eg. flickr. You might need
    # a subparser in that case.
    parser.add_argument('-s', '--source', action='store',
                        help='Source directory')

    return vars(parser.parse_args())


def is_image(filename):
    if not os.path.isfile(filename):
        return False
    filetypes = ['png', 'jpg', 'jpeg']
    if not imghdr.what(filename) in filetypes:
        return False
    return True


def get_photo(source, count=1):
    """Read the source dir, get some photos (defaults to 1, count might 
       be higer early in a relationship). """
    if not source or not os.path.isdir(source):
        raise MadnessException('Bad source')
    pics = [os.path.join(source, f) for f in os.listdir(source) if is_image(os.path.join(source, f))]
    warnings = []
    photos = []
    if len(pics) == 0:
        raise MadnessException('No photos available')
    elif len(pics) < count:
        warnings.append('Not enough photos, refill soon. Sending %s' % len(pics))
        photos = pics
    else:
        photos = [pics.pop(0) for i in xrange(count)]
    return photos, warnings


def mail_photos(photos):
    pass


def delete_photos(photos):
    [os.remove(pic) for pic in photos]
    

def main():
    args = parse()
    photos, warnings = get_photo(args.get('source'), int(args.get('count')))
    mail_photos(photos)
    delete_photos(photos)
    if warnings:
        raise MadnessException('\n'.join(warnings))


if __name__ == '__main__':
    sys.exit(main())
