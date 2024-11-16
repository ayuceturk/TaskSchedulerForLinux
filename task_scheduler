#!/bin/bash

# Task scheduler main menu
while true; do
    echo "Task Zamanlayıcısı "
    echo "1. Taskleri Listele "
    echo "2. Yeni task aç "
    echo "3. Task sil "
    echo "4. Çıkış yap "
    read -p " 4'ü arasından bişi seç: " choice

    case $choice in
        1)
            echo "Listelenmiş taskleri göster..."
            crontab -l || echo "Listelenmiş task bulunamadı."
            echo ""
            ;;
        2)
            read -p "Dosya adını gir: " script_name
	    echo "Zamanlayıcı seç (Saatlik, Günlük, Haftalık):"
            echo "1. Saatlik"
            echo "2. Günlük"
            echo "3. Haftalık"
            read -p " 3'ü arasından bir seçim yap : " freq_choice

            # Determine the cron schedule based on frequency
            case $freq_choice in
                1)
                    schedule="0 * * * *"  # Saatlik
                    ;;
                2)
                    schedule="0 0 * * *"  # Gunluk
                    ;;
                3)
                    schedule="0 0 * * 0"  # Haftalik
                    ;;
                *)
                    echo "Yanlış girim yaptın baştan dene."
                    continue
                    ;;
            esac

            # Add the task to crontab
            (crontab -l 2>/dev/null; echo "$schedule $script_name") | crontab -
            echo "Task başarıyla eklendi."
            echo ""
            ;;
        3)
            echo "Task Silme:"
            crontab -l || echo " Task yok ki ."
            echo ""
            read -p "Task no seç: " task_no
            crontab -l | sed "${task_no}d" | crontab -
            echo "Task başarıyla silindi."
            echo ""
            ;;
        4)
            echo " Çıkış Yapıldı ."
            exit 0
            ;;
        *)
            echo "Yanlış numara girdin."
            ;;
    esac
done
